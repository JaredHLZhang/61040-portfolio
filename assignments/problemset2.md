# Problem Set 2: URL Shortening Analysis

## Concepts for URL Shortening

### Contexts
The contexts is for helping to define separate domains of uniqueness, making each generated strings is unique. If the service supports multiple domains, each of these domains would be its own context. Within each domain, the nonces must be unique, but two different domains can reuse the same short string without conflict. Therefore, in the URL shortening app, a context ends up being the base URL or namespace in which shortenings are generated and stored.

### Storing used strings
If the system does not track what has already been generated, it will repeat strings and cause collisions in the short and target URLs. A counter plays the similar rule for exclude the existing items. For example, when the number 36 comes out means from 0-35 is already been used. Similar to that, a new string comes out because the system checked what other strings are used, and the new one is not used.

### Words as nonces
One advantage is that it is easy to remember and typing. Disadvantage is that words are limited in number, in order to keep unique, it will generate different words, if the generated word is not strongly related with the URL context, it will make user feel confuse.

## Synchronizations for URL Shortening

### Partial matching
Because generate is for generating a nonce in the correct namespace, which only need to know the context, and context is from shortUrlBase. TargetUrl is not in need in this case because it doesn't care what the eventual target page will be. However, register needs create the mapping from a short url to a target url, so it must have both the targetUrl and the shortUrlBase.

### Omitting names
This question actually I was confused in previous problem set, so for every arguments I write their variable name. After lectures and practice, now my understanding is that the omitted name only works when the argument name and local variable name are identical. For example, targetUrl can write as targetUrl because there is only one identical variable. However, if they are different. For example, shortUrlSuffix's variable is nonce, it will cause the people who reading this concept feel confuse about what variable this argument is conduct for.

### Inclusion of request
Because generate and register is system response to user's request. Request represent a trigger condition from the user to the system reaction. However, setExpiry is a system's processing based on previous reaction that already by triggered by the user, which not need require because there is no user action involved in this sync.

### Fixed domain
In this case the context will be only bit.ly, which means it does not need request shortUrlBase, so to implement this I will remove shotUrlBase from the concept, instead, I will use a fixed constant bit.ly as context.

### Adding a sync
```
sync expire
  when ExpiringResource.expireResource (): (resource: shortUrl)  
  then UrlShortening.delete (shortUrl)  
```

## Extending the design

### New concept designs:

#### Concept Ownership
```
concept Ownership
  purpose record and check the owner of each short link
  principle only the owner of a short link can view its analytics
  state
    a set of Ownerships with
      shortUrl String
      ownerUserId String
  actions
    recordOwner (shortUrl: String, ownerUserId: String)
      effect saves the owner of shortUrl as ownerUserId
    authorizeView (shortUrl: String, requesterUserId: String)
      requires Ownership(shortUrl, ownerUserId) exists and ownerUserId = requesterUserId
      effect succeeds if requester is the owner; otherwise the action cannot be performed
```

#### Concept Analytics
```
concept Analytics
  purpose maintain a counter of accesses for each short link
  principle each successful translation increments the counter
  state
    a set of Counters with
      shortUrl String
      count Number
  actions
    initCounter (shortUrl: String)
      requires no counter exists for shortUrl
      effect creates a counter with count = 0
    increment (shortUrl: String)
      requires a counter exists for shortUrl
      effect increases count by 1
    getCount (shortUrl: String): (count: Number)
      requires a counter exists for shortUrl
      effect returns the current count
```

### 2. Three essential synchronizations:

```
sync whenCreate
  when
    UrlShortening.register (): (shortUrl)
    Request.currentUser (): (userId)
  then
    Ownership.recordOwner (shortUrl, ownerUserId: userId)
    Analytics.initCounter (shortUrl)

sync whenTranslate
  when UrlShortening.lookup (shortUrl)
  then Analytics.increment (shortUrl)

sync whenViewAnalytics
  when
    Request.viewAnalytics (shortUrl)
    Request.currentUser (): (userId)
    Ownership.authorizeView (shortUrl, requesterUserId: userId)
  then
    Analytics.getCount (shortUrl): (count)
```

### 3. Feature requests:

**3.1. Allowing users to choose their own short URLs:** We can add a new request for customSuffix. If the suffix is available, it will then got to sync register. This new feature does not broke the original generate, but offer users another parallel option to custom their own short link.

**3.2. Word as nonce strategy:** It is another way of NonceGeneration. We can add a wordAsNonceGeneration feature to manage the word can or can not use. However, like the answer in the concept question, word as nonce has both advantages or disadvantages. Therefore, my idea is that maybe it can be an option for user that they can choose to use word if the word they want to use is available, if not available so just use the nonce that generated.

**3.3. Including the target URL in analytics:** I think this feature will involved an exposure of user's individual privacy information because target URL is more sensitive than shorter URL. So even we had the ownership authorization designed before, however, it's better to have a more personal certification like the MIT did with DUO for two factor authentication.

**3.4. Generate short URLs that are not easily guessed:** This is a nonce generate strategy, so in the NonceGeneration concept design, we can add a new state and action and apply them in sync that generate secure nonce using a mathematic way.

**3.5. Analytics visibility for unregistered users:** This feature I think is undesirable and should not be included because that is valid for user privacy. From company's perspective, it wish user to register, so a visible report will be an encouragement for registration. Therefore, this is undesirable feature for both company and registered users.

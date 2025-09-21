# Assignment 2: Problem Set 1: Reading and Writing Concepts

## Exercise 1: Reading a concept

### Answer to the questions:

**Invariants:** First one the that the total number of purchases is equally or less that request's number on the list. The second is that every purchase must correspond to an existing request in the same registry. I think the first invariant is more important because it is a system rule to prevent overselling and disorder between request and purchase. Therefore, it most affected by purchase because it enforces the invariant by decrementing the request count and requiring correct number of item before recording a purchase.

**Fixing an action:** Action removeItem. When the registry is opened and givers has already purchased some items, then the owner remove the one or more requests through removeItem, it may causes number of purchase more than total requests. Add a lockItem action, so if a item in the registry is already be purchased by a giver, the owner can not remove it from the registry.

**Inferring behavior:** Yes, it allows open and close repeatedly. Because from the design there are only active or not active states and action required depend on that. If I close it, it change to not active and not delete any registry. Therefore, there still has the registry and then it is not active which meets the require for open, so I can open again.

**Registry deletion:** Ah…as I just mentioned in last question. I think it is not required in practice. Rather than delete the registry, maybe delete request one by one on the list until it become empty is better or just close the registry is more reasonable.

**Queries:** For owner I think is the get the purchase summary see who buy which item. For givers is the available item see which request item is still available to purchase.

**Hiding purchases:** I will add a new state that is a hide purchases flag under a set of purchases with. Then add an action that a when an item purchased by a giver, the user can select to hide the item of purchase with the hide flag active.

**Generic types:** ID code like SKU are stable that it does not change when names, price, or other description about the item changed. Moreover, text can be really similar with two different items, but code can be different and it is the only code for that specific item. Also it is more detectable and easy to management in the backend system.

## Exercise 2: Extending a familiar concept

### 1. State
```
a set of Users with
    an username String
    a password String
```

### 2. Action
```
register (username: String, password: String): (user: User):
    requires: no User exists with this username
    effects: create a new User with this username and password

authenticate (username: String, password: String): (user: User)
    requires: a User exists with a username and match with the password
    effect: authenticate the user as the User
```

### 3. Essential Invariant
The essential invariant is that each username is unique so no two users shared the same user name

### 4. Email confirmation registration update

#### State
```
a set of Users with
    a username String
    a password String
    a confirmed Flag

a set of ConfirmationTokens with
    a user User
    a token Secret
    an expiration Time
```

#### Actions
```
register (username: String, password: String): (user: User, token: Secret)
    requires no User exists with this username
    effects create a new User with this username, password, and confirmed set to false; 
            create a new ConfirmationToken for this user with a fresh token (and expiration); 
            return the user and the token (the token is then emailed to the user).

confirm (username: String, token: Token)
    requires a ConfirmationToken exists for this username with a matching token, not expired, 
             and the user is not already confirmed
    effects set the user's confirmed Flag to true and remove the token from ConfirmationTokens.

authenticate (username: String, password: String): (user: User)
    requires a User exists with this username and password and the user's confirmed Flag is true
    effects return this User as the authenticated user.
```

## Exercise 3: Comparing concepts

### PersonalAccessToken [User]

**Purpose:** allow a user to authenticate without using their password, while limiting what actions the token can perform

**Principle:** a user can create one or more tokens, each with a secret string, expiration date, and selected scopes of access; the secret is shown once at creation and must be saved by the user; the token can be used in place of the user's password for GitHub services, but only with the rights granted by its scopes; a token may later be revoked by the user or automatically expire.

#### State
```
a set of Tokens with
    an owner User
    a secret Token
    a set of Scopes
    an active Flag (valid, used, canceled)
    an expiration Time
```

#### Actions
```
createToken (owner: User, scopes: Scopes, expires: Time): (token: Token)
    requires the owner exists and requested scopes are valid
    effects create a new active token with the chosen scopes and optional expiration, 
            generate a fresh secret, store only its hash, and return the token together 
            with the secret (shown once to the user)

revoke (owner: User, token: Token)
    requires the token exists, belongs to this owner, and is active
    effects set the token's active Flag to false

authenticate (username: User, token: Token): (user: User, scopes: Scopes)
    requires there is a token for this username whose secret matches, that is still active and not expired
    effects return the user together with the token's scopes
```

### Difference between password and token
I think token and password play in different roles: Tokens are designed for services like APIs, while passwords are for direct user login. You can have only one password but you can have multiple tokens for authentication. Tokens are scoped, limiting what they can do, unlike passwords which give full access. Tokens can expire or be revoked individually, whereas passwords must be reset for everything at once. The token secret string is shown only once at creation, unlike a password that a user repeatedly enters.

### Github page improve
In the Managing your personal access tokens page. It said "Treat your access tokens like passwords". However, for freshmen to the computer system, it will misguide them to think tokens and password are same.

## Exercise 4: Defining familiar Concepts

### ConferenceRoomBooking [User, Room]

**Purpose:** coordinate access to conference rooms so that only one group uses a room at a given time

**Principle:** a user selects a room and a time interval, and makes a booking if the room is available; the system records the booking and prevents overlapping bookings; the booking can later be canceled by the creator.

#### State
```
a set of Rooms
a set of Bookings with
    a room Room
    a Start Time
    an End Time
    an owner User
```

#### Actions
```
createBooking (room: Room, start: Start Time, end: End Time, owner: User): (booking: Bookings)
    requires room exists and no existing booking for this room overlaps within start to end time
    effects create a new Booking with this room, time interval, and owner

cancelBooking (booking: Bookings, owner: User)
    requires booking exists and owner is the booking's owner
    effects remove the booking from the state
```

**Notes:** The subtlety is ensuring that overlapping bookings are prevented, which requires precise definition of time intervals. Recurring bookings and group permissions are deliberately excluded to keep the concept minimal.

### ElectronicBoardingPass [Passenger, Flight]

**Purpose:** allow a passenger to hold a digital boarding credential that updates in real time as flight information changes

**Principle:** after checking in for a flight, the passenger receives an electronic boarding pass; the pass contains flight details (gate, time, seat, barcode); if flight details change, the pass is updated automatically; the passenger presents the pass at the gate, where its validity is checked.

#### State
```
a set of Boarding Passes with
    a passenger Passenger (my initial thinking is User, but I think Passenger is not User in this case, please clarify me if I am wrong)
    a flight Flight
    a seat Seat
    a barcode Token
    a status Flag
    flight details Details
```

#### Actions
```
issuePass (passenger: Passenger, flight: Flight, seat: Seat): (boardingPass: Boarding Passes)
    requires passenger is checked in for the flight and no valid pass already exists
    effects create a new BoardingPass with details from the flight and assign a unique barcode

updatePass (boardingPass: Boarding Passes, new detail: Details)
    requires boardingPass exists and is valid
    effects modify flight details (gate, time, etc.) in the pass

usePass (boardingPass: Boarding Pass)
    requires boardingPass is valid and corresponds to an active flight
    effects mark status as used

cancelPass (boardingPass: Boarding Pass)
    requires boardingPass exists and is valid
    effects mark status as canceled
```

**Notes:** Subtleties include real-time synchronization: the boarding pass is stored in both the airline system and the passenger's wallet. The barcode links to the backend for final validation, so duplication is prevented.

### AddressVerification [User, Address]

**Purpose:** confirm the identity or eligibility of a user by checking a supplied address against an authoritative record

**Principle:** a user provides an address; the system forwards this address to an authoritative source (such as a credit card issuer or phone company); the authority compares the provided address with the one on record and responds with a verification result; the application then decides whether to grant access or complete a transaction.

#### State
```
at the application: a record of Verification Requests with
    a user User
    an entered address AddressFragment
    a result Flag (pending, match, mismatch)

at the authority: a record of RegisteredAddresses with
    a user User
    a canonical address Address
```

#### Actions
```
submitAddress (user: User, addressFragment: Address Fragment): (request: Certification Requests)
    requires user is known to the application
    effects create a VerificationRequest and send to the authority

verifyAtAuthority (user: User, addressFragment: Address Fragment): (result: Flag)
    requires authority has a RegisteredAddress for this user
    effects compare fragment with canonical address; return result (match or mismatch)

recordResult (request: Certification Request, result: Flag)
    requires request exists and result is returned
    effects update the request's result Flag
```

**Notes:** The key subtlety is that state is distributed: part lives with the requesting application, part with the authority. The concept does not require either party to know the full state of the other—only that the comparison action yields a result.

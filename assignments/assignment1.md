# Assignment 1: Problem Framing

## 1. Domains

### List of Ten Domains
1. Long-distance relationships (LDR) & happiness
2. Relationship therapy & coaching
3. Affective computing in human-centered AI applications
4. Generative AI (AIGC) for emotional support
5. Social media influence on emotional well-being
6. AI companionship (NOT JUST TALK WITH AI FOREVER!!!)
7. AI in digital marketing and IP design
8. Fashion design with AI
9. Meditation practices for Gen Z
10. Work–life balance: planning & management

### Three Selected Domains with Explanations

**Long-distance relationships (LDR) & happiness**  
This domain is deeply personal to me. Over the past summer, I went through a four-month long-distance relationship with my girlfriend. It was a struggle: we experimented with LDR apps and searched for advice on Google, YouTube, and TikTok. Often these tools didn't help, and sometimes they made things worse by creating more pressure and effort. From this experience, I became determined to design a software solution that genuinely supports LDR couples—helping them sustain happiness rather than adding frustration.

**AI companionship (NOT JUST TALK WITH AI FOREVER!!!)**  
Recently, I have been exploring AI companionship platforms such as Tolen, Replika, and Character.AI. I even created some AI characters for fun. I also trust ChatGPT as a companion in solving problems. Yet I've noticed—and research confirms—that over-reliance on companionship AI can increase social isolation. On Reddit and TikTok, I found examples of people spending over eight continuous hours chatting with AI. I want to explore whether it's possible to design companionship AI that provides emotional support while encouraging users to connect more with real people, instead of endlessly talking to AI alone.

**Work–life balance: planning & management**  
Both in my own life and in my peers' lives at MIT and Harvard, I've noticed how difficult it is to achieve work–life balance. Classes, homework, thesis projects, job searches, and startups often dominate schedules. Research suggests that balanced play and relaxation can improve efficiency and creativity, but many of us fail to implement this balance in practice. I am interested in designing a tool that helps students and professionals create schedules that integrate productivity with recovery, making work sustainable and life more fulfilling.

## 2. Problems

### Domain 1: Long-distance relationships (LDR) & happiness
- Miscommunication without nonverbal cues – Couples lose tone and body language, leading to frequent misunderstandings.
- Low emotional resonance in digital interactions and quality time – Video calls and texts feel repetitive, failing to capture intimacy.
- Luck of experience and "skill" for handling LDR – Young couples like our age (college students) almost first time experience LDR in their life and most likely have no idea of handling the relationship in this struggle situation.
- Reliance on generic or unhelpful LDR apps (one more for this domain) – Existing tools often create more "tasks" instead of easing emotional strain.

**Selected Problem:**  
Miscommunication without nonverbal cues - because it is the most common and impactful issue for LDR couples when I search on reddit and LDR forum.  
Low emotional resonance in digital interactions and quality time - I'd like to include one more problem, because when I discussed this topic with four of my friends who have experienced or are currently experiencing LDR, they all highlighted this issue.

**Excluded Problems:** 3 (kind of therapy and life coach related), 4 (more about poor implementation than core emotional challenge).

#### Citation for Evidence
Google search showed that in 2024 long-distance is the top 1 issue for relationship problem in US. A study found that the better a digital communication medium was at eliminating miscommunication, the more positively participants rated their long-distance relationship quality (correlation r = .37, p < .01) This underscores concretely how the absence of non-verbal cues in digital communication (tone, facial expression, body language) leads to misunderstandings and reduced relationship satisfaction. Also an article mentioned GenZ LDR couples will have 30-45 mins video call time per day as their quality time in relationship.

#### Comparable Context
A section in the "Emotions in Virtual Communication" concept (e.g., in computer-mediated communication research) shows that CMC lacks paralinguistic cues such as gestures, emphasis, and intonation. People often overestimate their ability to convey emotion clearly in text, leading to more misinterpretation. This parallels the LDR challenge—when nonverbal cues are missing, even good intentions may be misread.

### Domain 2: AI companionship (NOT JUST TALK WITH AI FOREVER!!!)
- Helpful but risk of social isolation – People get emotional support from it but heavy users rely on AI more than real friends.
- Emotional over-attachment to AI – Users may treat AI as a substitute for human intimacy.
- Generic and shallow conversations – Current AI companions often feel repetitive and lack depth.

**Selected Problem:** Helpful but risk of social isolation – it is the broadest and most critical issue, supported by research and lived experiences. It's the double-edge sword for AI companionship.

**Excluded Problems:** 2 (related to isolation but narrower, also population is limited), 3 (technically solvable but not as socially urgent and design perspective).

#### Citation for Evidence
A longitudinal, randomized-controlled study made by Media Lab and OpenAI found that higher daily usage of AI chatbots, especially voice-based ones, was associated with increased loneliness, greater emotional dependence on AI, and reduced real-world socialization, particularly among heavy users.

#### Comparable Context
An article by Common Sense Media reported that 75% of teens have tried AI companion apps, and 20% spend as much or more time with AI than with real friends. Experts warn this can impair social skills and deepen loneliness. Also HBS review mentioned AI companionship become top1 use for LLM in 2025 and 31% of GenZ and Millennium start to use AI companionship.

### Domain 3: Work–life balance
- Overloaded schedules with poor planning tools – Students juggle many tasks without effective prioritization.
- Burnout due to lack of recovery time – Work dominates, relaxation feels "unproductive."
- Difficulty forming playful habits – People don't integrate fun or social breaks into their lives.

**Selected Problem:** Burnout due to lack of recovery time – because it directly impacts mental health and long-term productivity.

**Excluded Problems:** 1 (important but already tackled by many generic planners), 3 (secondary to the deeper issue of burnout).

#### Citation for Evidence
A 2025 study on burnout among medical students highlighted lack of time for rest and recovery as a key contributor to burnout. Another study on academic burnout among college populations emphasized that academic performance pressures drive high levels of anxiety and depression, which contribute directly to burnout.

#### Comparable Context
Quality student-support resources, for example university wellness centers at University of Georgia, underscore that burnout develops over months or years, and recovery requires time, self-care, and strategic schedule adjustments.

## 3. Stakeholders

### Problem 1: LDR miscommunication and less emotional connection in quality time
- Partners in LDRs – primary users struggling with misunderstanding and report less emotional connect in quality time.
- Therapists and relationship coaches – help clients repair damage caused by miscommunication and provide consultant on relationship support.
- Families and close friends – indirectly affected when couples are stressed.

### Problem 2: AI companionship isolation
- Users of companionship AI – benefit from support but risk over-reliance.
- AI developers & platforms – face ethical concerns about promoting healthy use.
- Mental health professionals – encounter clients who replace therapy or social contact with AI.

### Problem 3: Work–life Burnout
- Students and professionals – suffer reduced well-being and effectiveness.
- Universities and employers – impacted by poor performance and attrition.
- Friends/family networks – relationships strain when individuals are overworked.

## 4. Features

### Problem 1: LDR Miscommunication and less emotional connection
- An AI mediator – understand the context and help the couple to align the misunderstanding.
- A memory generator – An AI understand their communication context and help them generate some memory records in visual, which they always miss in long-distance (eg. no group photo, no visual memories)
- Adaptive communication coaching – Provides suggestions to improve understanding over time.

### Problem 2: AI Companionship but not causing social isolation
- Human-connection nudges – AI encourages users to reach out to friends/family when provide companionship (emotional support/therapist).
- Usage time caps & reflection breaks – Prompts users to step away after long sessions.
- Co-play features – AI suggests shared activities with real people (e.g., collaborative journaling).

### Problem 3: Work–life Burnout
- Balance planner with recovery slots – Enforces breaks and playful activities.
- Mood-based scheduling – Adjusts tasks depending on stress or energy levels.
- Community challenge groups – Encourages collective accountability for balance.

*(seems like some features across these three problems can be integrated)*
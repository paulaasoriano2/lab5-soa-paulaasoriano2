# Lab 5 Integration and SOA - Project Report

## 1. EIP Diagram (Before)

![Before Diagram](diagrams/before.png)

Describe what the starter code does and what problems you noticed.

---

## 2. What Was Wrong

Explain the bugs you found in the starter code:

- **Bug 1: wrong filter**
The problem was that the filter inside the oddFlow was wrong implemented because it lead pair numbers to enter, intead of impairs. This bug was fixed by changing the previous condition (`p % 2 == 0`) to the following: `p % 2 != 0`.

- **Bug 2: Gateway apuntando a evenChannel**:
The problem was that the gateway was sending negative numbers to the evenChannel, so those numbers which were impair negatives were considered as pair numbers. This made them skip the filter and the transformer. Firstly, it was thought to make the gateway apuntar to the numberChannel (`@Gateway(requestChannel = "numberChannel")`). However, this idea was discarded because it does not make much sense for the router to evaluate them as pai or impair numbers, as well as to pass through the transformation of the evenChannel if it is a pair negative number. The solution was to make the gateway apuntar to the oddChannel (`@Gateway(requestChannel = "oddChannel")`), so the negative numbers can go directly to the service activator without any unnecessary transformation.

- **Bug 3: oddChannel as a direct channel**:
oddFlow and SomeService were reading from oddChannel, which was a direct channel, so the impair numbers did not cross through the filter and the transformer. The solution was to make oddChannel to be a PublishSubscribeChannel (`fun oddChannel(): PublishSubscribeChannelSpec<*> = MessageChannels.publishSubscribe()`) instead of a direct channel in order to enable broadcasting.

---

## 3. What You Learned

Write a few sentences about:

- What you learned about Enterprise Integration Patterns
- How Spring Integration works
- What was challenging and how you solved it

---

## 4. AI Disclosure

**Did you use AI tools?**
The only AI tool used was ChatGPT

**Important**: Explain your own understanding of the code and patterns, even if AI helped you write it.

---


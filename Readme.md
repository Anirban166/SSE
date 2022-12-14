> Based on my reading of Ross Anderson's 'Security Engineering':

Laying the groundwork for SE is what the first chapter intends to institute, and I would say that it did a fairly good job of getting across the abstract or an overview of the field to me. I realize that this particular field of study focuses on computers and more specifically software and network security, but it inevitably depends on or interfaces with other forms of security (physical, for e.g.) as well.

Prior to reading about the established framework, I thought that selecting one or a mix of different mechanisms based on their assurance level in order to achieve the end goal or 'policy' could be sufficient to summarize the working of a security system in terms of the mentioned framework components. Yes, I never thought about *incentive*, as I previously considered that to be a separate point. After reading about the perspectives of the decision makers (may it be policy weavers or system breachers), the inclusion of that component started to make sense, and as to why it was interconnected with the others.

I liked the examples because they were simple enough for me to wrap in my head the possible scenarios in play. I feel they demonstrated a good form of 'incentive' for the attacker (financial profit from bank accounts, an advantage in warfare from military data breach and jamming, leveraging injury/disease/impairment/disability-based information from medical health records for very specific potential harm against individual patients, etc.), showcased realistic situations, and included a reasonable discussion on the operation and potential risks of such systems.

If I were to name one element from the reading that I found to be particularly insightful, it would be insider threats. The fact that employees themselves pose a high risk for the system that they deal with is really concerning. The point that I noted is that employees too in a cynical sense, are perfectly suitable to be humans that deviate from protocols for personal interests and that a certain degree of trust although exists, is not sufficient to determine a secure modus operandi from their ends.

Frankly speaking, I am not surprised that iniquitous behaviour could still arise from individuals at positions that generally either reflect trust (like a bank employee) or have severe consequences for going against expected behaviour for the sake of personal interests. Monitoring of work-related activity in that sense seems to be essential. This reminds me of the example in the summary (which I found to be interesting), where the definition of 'security' tends to be a polar opposite between the two entities (a corporation and the employees under it were the entities) - one concerning possible employee data breaches, and the other concerning 'privacy' of the employees, both in terms of monitoring such activity. This last part also gave me a concrete example to supplement or fortify my understanding that the terminology associated with security engineering is not static and changes with the context that we are dealing with.

> 09/07/22

I see that the discussion of car key fobs was in a way continued (initially discussed briefly in a few statements from the first chapter) or elaborated more on the third chapter (protocols). It talked about the devices called grabbers which in the old days were used with simple technology to store (from nearby) and replay (when the car owner is away) the signal emitted from the car key. It also mentioned about the pointlessness of using separate codes for locking and unlocking, or of increasing the code length (irrespective of the size, being able to brute force combinations for something is never a good possibility).

In order to understand this section (3.2 Password Eavesdropping Risks) through some visual aid, I'd suggest watching this [video](https://www.youtube.com/watch?v=5CsD8I396wo). The YouTuber covers some parts mentioned therein (and some new), like replay attacks which can easily break through static codes. He then mentions 'rolling codes' as the way to prevent this form of simple attack, wherein each time a different signal code is sent and received in between the key and the car, i.e. formerly used codes become invalid after the first use (underneath, I suspect it basically uses seeded random number generation on both the sender in the key fob and the receiver in the car which cyclically generates codes, with each code being unique and different from the previous one due to this rng). This too is suspectible, and he mentions the countermeasure for breaking this form of security by using a 'roll jam' attack. It uses two radios where the first one jams the signal sent by the key, and the second one records it. This effectively leads to an easy attack where the second radio sends the stored signals (which were previously unused as the first radio stopped transmissions from the key to the car) to the car in order to unlock it. Although it doesn't mentions it directly, the solution would be ideally to use some sort of cryptographic routine (potentially complex, but doesn't really need to be) to make only the car key fob communicate with the car via encrypted signals. (which makes the car theft possible only if the attacker has physical access to the keys - he/she could break the door, but will need keys to start the car anyways)

Ideally, protocols in the realm of security are constantly subject to change. (if they are not, then they'll probably be redundant in a few years, or sometimes even sooner)

Vulnerabilities are ever so existent, and curious entities will always find a way to break systems, or reverse engineer the patterns of security. Here's a [video](https://www.youtube.com/watch?v=VVJldn_MmMY) by Kingpin from L0pht that got me hooked into the scene early on.

> Responding to a person's thoughts

In a much broader sense, security theater can be applied to everything, given that security is never achieved completely, and at best, we only get a sense of it. I've dealt with systems requiring more than 2FA or two forms of auth, and these stacked layers of authentication definitely add up to limit potential breaches, although in the end its entirely possible to still break any number of security layers with proper preparation and resources.

<details>
<summary>A question for the same person</summary>
It seems that the world at present has to a certain extent, a degree of trust in SSL/TLS certificates that are being strictly enforced everywhere with https-based protocol connections. Under the hood, most browser to web-server (and vice versa) connections are encrypted using a 256-bit private key under modern cryptographic routines (I'm not entirely sure of the algorithms, but I presume they still use elliptic curves in most places, like ECDSA for digital signatures) that are deemed to be 'secure' for the moment.

Considering the modern-day implementations of SSL in our browsers (and not the former ones with major known bugs, or not Heartbleed for Apple's iOS), do you think they provide anything else apart from a sense of security when surfing the internet?
</details>

> Access protocols for reservations in commerical aviation

Modifying reservations for booked flights (changing itinerary or details for passengers/services, cancellation of the trip, etc.) is something that should either have a decent layer of security, or a few layers of authentication to avoid unwanted access. But it tends to not be the case for both these options.

The air travel sector is one which usually requires a decent level of security, but I???m still surprised that till date all airlines that I have travelled with only rely on the combination of a short alphanumeric string (typically 6 characters long) and my surname to provide one with access to my flight details with modification capabilities. (compare that with the physical security in the airport, which is relatively better)

I've seen people post plane tickets on social media in real-time (i.e., before their flight's departure and not after the trip) that contain both their surname (although most people would already know of their full name anyway so knowing this is usually a no brainer) and confirmation numbers, which makes them vulnerable to have direct changes to their flight by an outsider, such as cancellation of their reservation itself at the worst. This has actually happened several times in the past. While most travellers nowadays are aware of this, they still tend to share their confirmation numbers to online groups or print shops, which makes this minor security breach act very feasible.

I've never been affected by this or have shared details online or to people I don't know/trust to make it possible in obvious terms, but I still specifically request airlines to include another layer of authentication (nobody would usually care, but the confirmation number can be practically brute forced if the airlines' API doesn't rate-limit attempts to check a flight - and that too is usually based on the IP address for a session, which can be changed effectively for an attack, unless there are methods for shadow blocking via use of device addresses), which I usually get to be a previously recorded security question or passcode when trying to access my flight details online, or other personal details while trying to access over the phone. Depending on the airline's protocols or how they operate and deal with this, this additional layer of authentication may vary, and for some there may even be none!

No airline that I'm aware of establishes a lock that guarantees that a flight cannot be cancelled, for good reasons - one being the reasonable aspect (you should have the option to cancel if you really require to do so for whatever rationale that arises) and the other being the profitable (for them) one (the airline system always assumes that you might not be available even when you booked and are in fact till the last moment - this is what leads to overbooking of a flight). Thus, it becomes all the more important to enforce this additional step.

> Stolen OAuth Access Tokens

[Here's](https://thehackernews.com/2022/04/github-says-hackers-breach-dozens-of.html) a recent data breach reported by GitHub and published at Hackernews.

(I also received an email from GitHub at the time this was reported, notifying me of the potential data leak, given that I was using Travis-CI to run package checks for one of my projects, and presumably also since I had two deployments up at Heroku as well, both linked via GitHub repositories - much like mentioned towards the end of that post, or in accordance to what GitHub said about notifying the known-affected/victim users)

As disclosed therein, an attacker abused stolen OAuth user tokens that were formerly issued to two third-party OAuth integrators, Heroku and Travis CI. The attacker was able to download data from dozens of organizations, which included private data not meant to be disclosed elsewhere, within the scope of what those services required from those private repositories. This is a direct breach of confidentiality.

For quick reference, the very definition of the term from the very first chapter of Anderson's SE is:

'*Confidentiality involves an obligation to protect some other person???s or organization???s secrets if you know them.*'

In this case, the data breach included organization secrets (like GitHub secrets or tokens for an organization), which GitHub uses for authentication to CI/CD services and deployment hosting services. This in turn means those services can be accessed under the organization's name, and the attacker can gain access to logs and valuable insider insights.

Personally, I don't think I have been affected by this in terms of any noticeable concerns that I can visibly see, but I definitely suspect that companies whose CI/CD pipelines export and save data in between those services could have their data compromised (and this really depends on what type of data they are dealing with).

In terms of Integrity, maintaining the trustworthiness of these GitHub secrets entirely depends on the bridge between the platforms (i.e., GitHub and Travis/Heroku), and future violations would definitely downscale the integrity that has been established over time. As for availability, the consistently and readily accessible nature of those services wasn't really affected for the customers, may it be individuals like me or a bunch from organizations/companies that use GitHub. It's more of an information leak allowing an outsider access to platform data, and not a bug that breaks things.

> Responding to a person responding to me

*Context: Knowing that your data might have been leaked could affect how future clients trust using a site/program.*

I've read somewhere that in addition to possible new clients swaying away from the decision to use those services, some former customers left the platform as well after this incident. Sidenote: I'm still using Heroku, but I'll be leaving it soon since it won't be free starting November 28th this year :)

A good security breach is all it takes to bring down the reputation (maybe not completely, but in an impactful manner, certainly) and trust-factor for a company/product providing a service.

> A clarification

This form of authentication is either for a good period of time (like we can login to NAU for a week or so on a specific browser or client) or it is a 'one-time' thing required only for the first use when you connect (say, your GitHub account and the select repositories including private ones) to these platforms (like I don't personally authenticate time and again for any of my code coverage or unit testing workflows after the initial connection with CI/CD platforms, thanks to the token supplied by GitHub Secrets which automates this OAuth procedure for me). The latter seems to be the case here.

> Apple's 'Heartbleed' vulnerability: https://heartbleed.com/

During the month of February in 2014, Apple pushed a security update that affected the transport layer security protocol via SecureTransport for iOS (version < 7.0.6) and even OS X (version < 10.9.2) that basically allowed anyone on the internet who used that version of OpenSSL (which is a software library that secures communication over computer networks, and this was Apple's implementation of it) to access or read the memory of the servers that hold information for the web (all connections that went through that particular OpenSSL version). This potentially allowed attackers to eavesdrop on communications over websites or applications using that TLS protocol since the encryption could be bypassed, and thus they could also steal data directly from the services/users and impersonate them.

The vulnerability leverages the additional `goto` statement that comes after the second if-conditional in the function which verifies the exchange of signed messages: (signed using a key given by some encryption scheme)??
```c
static OSStatus
SSLVerifySignedServerKeyExchange(SSLContext *ctx, bool isRsa, SSLBuffer signedParams, uint8_t *signature, UInt16 signatureLen)
{
	OSStatus        err;
	...

	if ((err = SSLHashSHA1.update(&hashCtx, &serverRandom)) != 0)
		goto fail;
	if ((err = SSLHashSHA1.update(&hashCtx, &signedParams)) != 0)
		goto fail;
		goto fail;
	if ((err = SSLHashSHA1.final(&hashCtx, &hashOut)) != 0)
		goto fail;
	...

fail:
	SSLFreeBuffer(&signedHashes);
	SSLFreeBuffer(&hashCtx);
	return err;
}
// Link to the full code: https://opensource.apple.com/source/Security/Security-55471/libsecurity_ssl/lib/sslKeyExchange.c
```
Now `goto` is in itself unconditional, but the intent of that particular `goto` was to be inside that if-conditional and to execute only when the `update` method for the SHA1 hash object does not return a value that would make `err` to be 0. The `goto` for the signed parameter check (again, the second `if` statement) would not be executed if the encryption is not met, which is what we would usually want. But since the second one is not inside the `if` scope, it gets executed irrespective of the value of `err` (or even when the update method is not successful) and jumps into the `fail` label, which basically returns the status to be positive always, and the signature verification thus never fails. (meaning the encryption here is meaningless)

At present, I think that this sort of vulnerability can be fairly easily detected through a static analysis tool (given that it's just something out open in plain source code) or with a compile-time check which ascertains that `goto` statements do not lie out of a branch (which I think would be a custom rule, but it's recommended to write a static analysis tool for one's use case software system than to rely on the standard rules that apply to any project for a targeted language). One way to do this would be to look for all `goto`s to fall positive under branch coverage.??

> Static Analysis

The goal of static analysis is to find errors (the usual types such as syntax and logical ones, or at times, the more subtle ones like resource leaks) and possible bugs which can be deciphered by a direct source code analysis at compile time. The usual steps for modern day tools that do this involve parsing code, annotating a Control Flow Graph (CFG), walking through that CFG looking for bad patterns, and reporting them to the developer at the end of an analysis session.

Yes, there is no guarantee that what you look for during the compilation time would be a correct representation of something that is indeed wrong (and not just mere stylistic changes), and thus static analysis usually tends to produce a lot of false positives, or 'bugs that the program doesn't actually contain'. That being said, false positives or approximations of what one's code might do during runtime may not always necessarily be incorrect, as it is based on control flow analysis of source code and there may be subtle bugs which may not appear to be bugs directly. Not to mention, it is better than nothing right? For however many false positives that may occur, getting a single valid bug out of the use of static analysis tools is in itself what I believe makes those tools worth it for use in projects.

Neil MacIntosh's CppCon talk ('15) was pretty insightful. Developers often make simple mistakes in their code that are often left unattended either due to a hit-or-miss in logic (like setting the state of a system to on or off, as shown in his second example) or something similar but more hard to debug (like the first example in the video where the first argument to `memset()` wasn't a memory location, quite similar to what novice C programmers also do with `scanf()`/`fscanf()`, or wherever so an address may be required)

From the entirety of the sixty minutes, what I liked the most was that he mentioned how those tools execute quick enough to fit in the developers' *inner loop*, which becomes critical as many avoid these tools just thinking they would consume more time than one would take to figure the bug themselves, or more time than they would like to spend debugging on. (on a sidenote, this reminds of when I discussed with my mentors in JPL how the CMake build system was taking a lot of time to build unit tests for a project, wherein just using simple make or even a shell script for compilation and linking to build would have been much faster - this is quite similar, wherein how fast the static analyzer runs is critical for acceptance from developers that do not like to waste time)

It was also interesting to gather that static analysis tools can directly help in performance-critical code, leading to optimization in suitable cases (for e.g., that talk mentions avoiding cross-process calls and busy loops that are possible to detect through static analysis). The annotations that were incorporated in the source code for `makePacket()` (which was a 'simplistic representation' of the Heartbleed bug as it dealt with breaching reliance in network code to be safe, like the presenter claims) were also something that at a first glance looks extra, but it really helps not only the tool to detect but also a human to read the code (i.e., once he or she has spent enough time to understand the syntax/structure of those 'annotations') better, instead of going through the comment that was there in place. (I say this because in certain codebases, comments are not well-translated enough into code for the reader to think and be concerned about while reviewing)

There's an interesting static sc-analyzing tool named 'UNO', with the abbreviation's expansion being three common errors (uninitialized variables, nil-pointer dereferences, and out-of-bounds array indexing) that it specifically targets for C programs. It's main point of selling is that it allows the user to define application-specific properties instead of going with a predefined set of rules to detect these. This not only helps with flexibility, but also makes this a good tool to check for those three kinds of errors in almost any C program. A literative review is done with other known static sc checkers to demonstrate that it is the first one among them to have annotations that assist in the checking process, with access to relevant def-use information via UNO's dataflow analysis engine. It has proven to be practical too, as it found the types of bugs it targets in commerical software such as Sendmail and Unravel.??Like a presenter using the functional language Racket to build a simple static analyzer mentioned early on, SWEng doesn???t have any predictive models like other forms of engineering, so it's hard to write or rather 'engineer' programs that are bug-free and secure. (not too inclined to agree on the 'too slow' point)

In general, the ability to define custom static analysis properties is extremely useful for a proper analysis of the source code for a specific project. The pre-determined rules for bug checks do not always reveal the defects that a project may have due to non-standardized programming constructs, or behaviour outside of the enlisted crtieria. User-defined properties allow one to cater the checks to their application project/program, based on the constructs used therein, and based on the patterns it follows.

> Static analysis check for capturing conditional assignment values from ternary operators

One simple example of a static analysis check implemented underneath as a regular expression can be that of a comparison in between two conditional values to be equal, when assigning to something with a ternary operator.
Casually thinking, the Perl-based regular expression to capture that can be something simple like "\?(.+):(.+)", where the two capture groups (a pair of parentheses denote a capture group, for the characters you would like to store for use/checks later) if deemed to be equal, can signify as a static analysis check that notifies the user that either way of the condition flow, the same value is being assigned, meaning that the conditional assignment being imposed by the ternary operator is meaningless.
This pattern can be used inside the grep function in your language of choice, provided there is an implementation. I used R to test such regular expressions recently (the only difference for that pattern is that for escaping metacharacters or reserved symbols like the question mark I used above, you will need two backslashes instead of one in R) and I use `grep(data, pattern)` to obtain the matches of such instances in my R code where there are ternary operators being used, the definition of which comes from a user-defined function (something like [this](https://stackoverflow.com/a/8791496), as R doesn't have a default one). `data` would be my R script file parsed as a string, and `pattern` would be my string that I declared above.??

Similarly, such checks can be used for the conditional itself, wherein multiple values separated by logical conjunction and disjunction must not evaluate to the same thing, as that too would be redundant. Using capture groups in a regular expression and playing with them post capture is essential to detect such code segments. The fact that many static analysis rules (mostly syntactical, and especially with ones involving keywords) can or do in fact use regular expressions (without requiring control flow analysis) to get the patterns is something I find to be pretty cool, as one can implement such checks himself/herself without needing to write a static analysis tool! (thus avoiding slightly more complex stuff like parsing a CFG, making annotations, etc.)

Note that RegEx-based static analysis checks only work if the syntax matches exactly to the established pattern, and cannot really be used to go for logical errors or deeper control flow problems (which may for instance, include resources problems like segfaults or memory leaks - some of which can be caught using analysis of resource allocations and deallocations using trees with proper static analysis tools). Distinguish between reserved words or constructs in the entirety of the codebase isn't super easy as well (for e.g., the keyword can be within a print statement, macros of that name may exist, some library may have that name for a function, etc.), unless the pattern is complex enough.

Indeed, writing a static analysis tool from scratch is quite a bit of work. One would need to build AST parsers, pre-defined and source code based (dynamic) trees, symbol table builders, control flow analyzers, and what not, in top of making it specific to your case. But in terms of profit, it would not only bring you the required bug checks, but it would also immensely help one by providing deep knowledge of analysis testing and problems with codebase-specific constructs, in addition to making it easier to build similar testing tools in the future.

> Regarding incorrect device to IPA mapping, a vulnerability I decided to elaborate a tad on

One critical vulnerability in the largest (several million lines of code) open-source project ever (the Linux operating system or rather the Linux kernel, with respect to the source code) was discovered late, much after the code already caused problems in that version of the OS and subsequently, the enormous number of projects that used it. This critical bug was caused due to bit shifting of a unsigned 32-bit integer, followed with expansion to a 64-bit equivalent which makes the shifted integer partly lose significant bits on the higher end and therefore have incorrect values. This affected device memory translation for virtual machines running Linux with more than 4GB of address space (which is almost all VMs nowadays), and had a severe implication - incorrect memory values being mapped.

Here is the [fix](https://github.com/torvalds/linux/commit/ca09f02f122b2ecb0f5ddfc5fd47b29ed657d4fd).
Basically, they first cast the unsigned 32-bit integer to a 64-bit one early on (notice the explicit `(phys_addr_t)`) and *only* after this cast bit shifts are done (`... << PAGE_SHIFT)`) to prevent loss of higher-value bits. (I'd suggest reading the commit message, as it is helpful and succicntly summarizes the fix!)

> Responding to a person responding to me (2)
 
I think Clang-Tidy would still be helpful for larger projects since it has a good collection of rules (including some complicated C/C++ coding constructs) it checks for to root out bugs (along with stylistic changes, but they can be filtered), but it might take a while for the static analysis to complete. It is usually ran as a check after compilation in CI services (most projects on GitHub run it along with a GitHub action for e.g.), so I'd recommend to first fix any compilation warnings (just because Clang-Tidy and most static analysis tools do warn on compiler complaints firsthand) and to not use it with the local setup (instead, use a separate workflow) of a build system (for e.g.,??[here's](https://developers.redhat.com/blog/2021/04/06/get-started-with-clang-tidy-in-red-hat-enterprise-linux#integrate_clang_tidy_into_your_build_system)??a snippet for setting it up with make) when using it for larger projects.

Trailing whitespaces also remind me of unicode characters which are rendered as invisible (including ones which are binary) and very hard to find unless you use a static analyzer or your compiler/interpreter is smart enough to flag them appropriately. (or you use hexdumps :)

> DeepState

DeepState, in a nutshell, is a testing tool consisting of a static library paired with a collection of fuzzers and symbol execution engines (which the developers commonly refer as to the 'backend'). The core work is still done by these tools that are integrated, but it becomes a lot easier to invoke them by command line executors (which are just python scripts underneath), and to write unit tests using reasonable constructs that DeepState introduces (and not to mention, the syntax is the exact same as Google Test, meaning you don't have to change that syntax if already using the popular test suite that is much commonplace anyway). Among all, I like DeepState's OneOf construct the most since it helps one to include various rules (as a lambda each) and execute one of them randomly, which tends to be extremely helpful when testing intersection of different behaviours in random sequences.

I enjoy reading Alex's blog posts (worded pretty well) and although I've come across them before, I just read both parts of 'Fuzzing an API with a DeepState', which goes deep enough to measure and demonstrate the usefulness of the tool, pulling context and starting off from John Regehr's take on the same.??

In general or when thinking about what a fuzzer actually does, I wouldn't say DeepState does anything *extra* than just making it easier for the fuzzers to be set up, and then to execute them (either one among all or in ensemble fashion) in a straightforward manner. However, there are other differences in how things are setup for the programmer, such as unique (i.e., DeepState-specific) functions and intuitive constructs to help the developer in creating tests, and to provide replacement for generic wrapper functions that are used in fuzzers (for e.g., functions that generate a random number of a particular type in a range for instance). There is also the structural difference in the way how typical DeepState routines work, which makes them closer to unit testing (generalized, indeed) more of than fuzzing.??

Performing a proper triage on crash results and finding the actual vulnerability post a fuzzing session still depends on the user's expertise, and is similar to a manual review of the fuzzer results without the use of the tool. Also worth noting that irrespective of the convenience imposed, using DeepState practically still requires familiarity with the system being tested (or more so a good understanding of the codebase under test - its purpose, the constructs used therein, etc.), which often means it can be hard to use the tool on a complicated system when lacking proper understanding of the latter. In contrast, using fuzzers directly could be relatively easier due to ease of provisioning the input. (no need to create a test harness!)
To elaborate, a standalone fuzzer usually takes just a bunch of files with test cases as input for the corpus, but for DeepState the input is sort of a structured program (doesn't include the main function since it is still in essence, a harness), which tends to be necessary as this helps the user to write unit tests. (as to how the fuzzer would see these unit tests as proper input, is left to DeepState's code)

Some unit tests are written very well, but it can be non-trivial to integrate them with a fuzzer appropriately. That's a core thing DeepState attempts at solving (essentially doing a property-based unit test that is being thrown into a fuzzer or SE engine), apart from providing other [features of significance](https://github.com/trailofbits/deepstate#overview-of-features).

> DROWN

'Decrypting RSA with Obsolete and Weakened eNcryption' is a critical software exploit which results in catastrophic consequences that involve breaching data from the entire server as encryption becomes pointless.??It involves HTTPS, with a good proportion of web servers being vulnerable to the exploit that allows attackers to force those servers to use an older, purposefully less secure version of SSL/TLS. By doing so, the attacker can more easily decrypt the older and weaker encryption, accessing data obtained in a classic MITM attack.

The exploit relies on the web server supporting SSLv2, a much older version of TLS, coupled with the fact that the same private key can be used in other servers with that same TLS connection. These are red flags when applicable for a web server, indicating that it's vulnerable to this exploit and can lead to serious damage (leak of any sensitive and secret information such as passwords and tokens) as this allows an attacker to decrypt even modern TLS connections between up-to-date clients and servers by sending probes to that server that supports SSLv2 and uses the same private key.
(link which tells the story and has more information on this specific exploit/vulnerability: https://drownattack.com/)

> Classification of vulnerabilities

For a binary classification, bugs on the extreme end are either ones that pose a major threat to software security and must be fixed immediately upon discovery (which may involve events like shutting down an entire server or system until it's resolved), or ones that are moved to the 'todo' or put on the back burner and are handled in a casual manner when time permits, as they are ones that are not easy to leverage, and even when exploited, the consequences aren't too serious to be concerned with for the developers/maintainers.

> Code review 

Something which is always essential, especially before releasing code out in the wild. I simply cannot think of any reason why code reviews can be bad at any point for a practical application. Sure, it might be time consuming but the least you get is to know your code better, and as the best outcome, you find real bugs that you potentially missed out on while writing the program, thereafter resulting in a revision of the application for the better.

All forms of review, may it be manual (one programmer reviews it all, pair programming style, a full team of programmers to review, etc.) or automatic (a review provided by static analysis tools that are integrated to the toolchain post-building the application, for e.g.), are always a good thing to have. On that note, one should not be entirely reliant on all vulnerabilities to be always uncovered during a code review of their own application if it involves a lot of external logic or importing code from other libraries and systems - one should be flexible to test other's code as well, like for e.g. the author of Bug Hunter's Diary found vulnerabilities by reviewing code coming from practically used software that were written by other developers)

> Bug Hunter's Diary

As a chronicle full of explorative software reviews, detailed exploits, triage, and reverse engineering episodes, this book and especially its personal diary based format was refreshing for a change in reading (instead of delving more into research papers for instance), whilst the material was kept lucid and educational or informative for both developers and prospective bug hunters.

The first chapter gave a brief introduction to 'Bug Hunting' and discussed a bit regarding motivations for the same, common techniques (i.e. static and dynamic variants, with the author's preference being the former) and tools (more specifically debuggers and disassemblers) used in the process, a bit on fuzzing and memory errors, and then through one/two paragraphs each, a few very specific topics such as potentially vulnerable code locations (near unsafe functions in libraries for the e.g. that the author primarily takes upon) and instruction pointer based control gain (end result past this point being arbritrary code execution for a proper exploit, for what the author follows).

The second chapter is focused on a bug in the VLC media player that the author found (dates back to '08, as per the diary record), with detailed steps he performed in order to potentially discover the vulnerability, and how he exploits it (again, he does so with reference to what he talked about in chapter one, such as finding paths to reach to/near the vulnerable code's location and later gaining control of the instruction pointer to execute commands as he wills, for which he mentions to have used the jmp reg technique for this one). I like how the author talks about various ways of disclosing the bug (if I ever so happen to discover one, I've always wondered what would be my options!), out of which he choose the coordinated manner. To help in writing code less prone to bugs, it's insightful to look at the 'lessons learned' section for each chapter as well.

Chapter seven is yet another interesting hack delivered well as a story in the format that the author has been following. He was able to make the OS X kernel (XNU version, with FreeBSD version < 4.4) panic and lead to a crash with his program that had just eleven lines of code (targeting the kernel code where IOCTL requests are handled), whilst executing without any privileges (which does count as an privilege escalation!). After taking control of the EIP (following his sequential steps for an exploit), he was also able to achieve arbritrary code execution at the kernel level as written in the text towards the end of section 7.2. (he mentions the steps involved therein; no code though as he claims to abide by the law by not publicizing that)

> Inputs

User inputs could very well be equivalent to the definition of trust issues, as they can be in a form that is easily subjected to risk (most common being no checks for validating inputs in one's program) especially if they can be code itself or if they can manipulate the logic in one's program directly. SQL queries are a perfect example of this.

[This](https://dl.acm.org/doi/10.1145/1390630.1390661) paper introduces an automated input test generation algorithm (with constraint resolving) to find bugs in real world web applications written in PHP which previously couldn't be found out through the latest and greatest of static analysis tools (primarily because of dynamic features in that interpreted language which inhibit proper analysis) and the standard concolic testing procedures. (It was successful in detecting known SQL injection vulnerabilities in open-source tools such as Mantis and Mambo)

> XSS

Cross-site scripting involves injection of a malicious script or code into trusted web applications or websites that have exploitable vulnerabilities. A successful attack usually accesses session tokens and cookies retained by the browser when a user used or is using a site,??which allows the invokers to leverage someone's logged in sessions for bypassing authentication.

During Fall '18, a high-profile hacker group known as Magecart targeted British Airways and successfully exploited a XSS vulnerability in their website, feeding upon a vulnerability in a JavaScript library called Feedify. The attackers successfully stole credit card data (direct breach of confidentiality) from thousands of transactions before the breach was discovered (380k to 500k was the reported number of users affected). They wrote a 22-line script to send customer data to one of their servers, whilst keeping the domain name alike to that of British Airways. The fake server also had an SSL ceritificate, which is probably the reason why users had trust when they were making transactions through that website.??

It seems like that library is integrated so it can collect feedback from the users/customers of the British Airway's site. Now while the scope might seem minimal with that, feedback is usually always prompted for collection after transactions and that means there is always a call to Feedify's servers, where the code they had was exploited by MageCart's malware, making its way to the source script and injecting the malicious modifications.

Static analysis might have been useful if the analyzer had access to read the source code of that imported JS library (which in ordinary conditions would not be open-sourced I reckon, but then integration testing is super important, especially for sketchy services).

> Coverage

I view the process of measuring code coverage as an essential part of the testing routine, although the metric in itself does not speak volumes. In general, the quality of tests written are far more important than just writing tests that cover all or most of one's code.
This comes from my previous experiences of measuring coverage for R and C++ code using tools and APIs before, including the integration into CI/CD pipelines for automatic code coverage report generation based on updates to a codebase.

However, fuzzers utilizing code coverage as a metric for guidance (greybox or coverage-guided fuzzers i.e.) in their instrumentation are usually better off than ones that do not trace for new paths via coverage-based feedback (essentially missing out on parts of the target program where the fuzzer wasn't able to venture into). As a heuristic in fuzzers thus, it's more cashmoney.

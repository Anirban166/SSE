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

The air travel sector is one which usually requires a decent level of security, but I’m still surprised that till date all airlines that I have travelled with only rely on the combination of a short alphanumeric string (typically 6 characters long) and my surname to provide one with access to my flight details with modification capabilities. (compare that with the physical security in the airport, which is relatively better)

I've seen people post plane tickets on social media in real-time (i.e., before their flight's departure and not after the trip) that contain both their surname (although most people would already know of their full name anyway so knowing this is usually a no brainer) and confirmation numbers, which makes them vulnerable to have direct changes to their flight by an outsider, such as cancellation of their reservation itself at the worst. This has actually happened several times in the past. While most travellers nowadays are aware of this, they still tend to share their confirmation numbers to online groups or print shops, which makes this minor security breach act very feasible.

I've never been affected by this or have shared details online or to people I don't know/trust to make it possible in obvious terms, but I still specifically request airlines to include another layer of authentication (nobody would usually care, but the confirmation number can be practically brute forced if the airlines' API doesn't rate-limit attempts to check a flight - and that too is usually based on the IP address for a session, which can be changed effectively for an attack, unless there are methods for shadow blocking via use of device addresses), which I usually get to be a previously recorded security question or passcode when trying to access my flight details online, or other personal details while trying to access over the phone. Depending on the airline's protocols or how they operate and deal with this, this additional layer of authentication may vary, and for some there may even be none!

No airline that I'm aware of establishes a lock that guarantees that a flight cannot be cancelled, for good reasons - one being the reasonable aspect (you should have the option to cancel if you really require to do so for whatever rationale that arises) and the other being the profitable (for them) one (the airline system always assumes that you might not be available even when you booked and are in fact till the last moment - this is what leads to overbooking of a flight). Thus, it becomes all the more important to enforce this additional step.

> Stolen OAuth Access Tokens

[Here's](https://thehackernews.com/2022/04/github-says-hackers-breach-dozens-of.html) a recent data breach reported by GitHub and published at Hackernews.

(I also received an email from GitHub at the time this was reported, notifying me of the potential data leak, given that I was using Travis-CI to run package checks for one of my projects, and presumably also since I had two deployments up at Heroku as well, both linked via GitHub repositories - much like mentioned towards the end of that post, or in accordance to what GitHub said about notifying the known-affected/victim users)

As disclosed therein, an attacker abused stolen OAuth user tokens that were formerly issued to two third-party OAuth integrators, Heroku and Travis CI. The attacker was able to download data from dozens of organizations, which included private data not meant to be disclosed elsewhere, within the scope of what those services required from those private repositories. This is a direct breach of confidentiality.

For quick reference, the very definition of the term from the very first chapter of Anderson's SE is:

'*Confidentiality involves an obligation to protect some other person’s or organization’s secrets if you know them.*'

In this case, the data breach included organization secrets (like GitHub secrets or tokens for an organization), which GitHub uses for authentication to CI/CD services and deployment hosting services. This in turn means those services can be accessed under the organization's name, and the attacker can gain access to logs and valuable insider insights.

Personally, I don't think I have been affected by this in terms of any noticeable concerns that I can visibly see, but I definitely suspect that companies whose CI/CD pipelines export and save data in between those services could have their data compromised (and this really depends on what type of data they are dealing with).

In terms of Integrity, maintaining the trustworthiness of these GitHub secrets entirely depends on the bridge between the platforms (i.e., GitHub and Travis/Heroku), and future violations would definitely downscale the integrity that has been established over time. As for availability, the consistently and readily accessible nature of those services wasn't really affected for the customers, may it be individuals like me or a bunch from organizations/companies that use GitHub. It's more of an information leak allowing an outsider access to platform data, and not a bug that breaks things.

> Responding to a person responding to me

*Context: Knowing that your data might have been leaked could affect how future clients trust using a site/program.*

I've read somewhere that in addition to possible new clients swaying away from the decision to use those services, some former customers left the platform as well after this incident. Sidenote: I'm still using Heroku, but I'll be leaving it soon since it won't be free starting November 28th this year :)

A good security breach is all it takes to bring down the reputation (maybe not completely, but in an impactful manner, certainly) and trust-factor for a company/product providing a service.

> A clarification

This form of authentication is either for a good period of time (like we can login to NAU for a week or so on a specific browser or client) or it is a 'one-time' thing required only for the first use when you connect (say, your GitHub account and the select repositories including private ones) to these platforms (like I don't personally authenticate time and again for any of my code coverage or unit testing workflows after the initial connection with CI/CD platforms, thanks to the token supplied by GitHub Secrets which automates this OAuth procedure for me). The latter seems to be the case here.

---
layout: post
title: Hidden Illicit User Interfaces in Apps
description: Apps with hidden user interfaces obscure their behaviour from the vetting teams of the app stores they target and from users unaware of the secret functionality. Those who are aware...
date:   2021-01-18 13:00:00 +0000
image:  '/images/posts/2021/hidden-illicit-ui-music-player-app.png'
tags:   [malware, iOS, android, research]
---

<style>p { text-align: justify; }</style>

This post discusses hidden illicit user interfaces (UI) and the challenges they pose for users and researchers. I was interested in the use of hidden UI for non-malicious purposes (but still illicit, i.e. against App Store ToS), here's a short introduction.

Apps with hidden user interfaces obscure their behaviour from the vetting teams of the app stores they target and from users unaware of the secret functionality. Those who are aware of the hidden functionality are paid a pittance for conducting in-app actions designed to exploit other users. Below we discuss an illicit iOS app which obscured a hidden UI enabling a covert community of crowdturfers to boost App Store apps from within a fully functional music player app. 

Most often, illicit user interfaces target the user, looking to steal private information extort, defraud and spread malware. On the Android platform, this type of illicit behaviour is often observed. For example, the Svpeng banking trojan. The svpeng trojan is capable of several attack scenarios aiming to obtain enough information to steal money. It has been observed employing extortion and ransomware tactics in addition to more subtle methods [<a href="#2">2</a>][<a href="#4">4</a>][<a href="#5">5</a>]. Here, we discuss the strain of svpeng which employs activity hijacking (i.e. an illicit UI) as seen below. Figure 1 shows a context-sensitive overlay within the genuine Play Store app (2014), prompting the user to enter financial information. 

<div style="text-align:center;"><img src="/images/posts/2021/svpeng-ui.png" alt="Svpeng banking trojan overlay intercepting financial information." style="width:250px; padding-bottom: 10px;"/></div>

<p style="text-align: center; font-style: italic;">Figure 1: Svpeng overlay intercepting financial information.</p>

The scale of threat differs greatly between Android and iOS ecosystems. According to F-Secure 99% of all malware developed for mobile operating systems is built for Android [<a href="#6">6</a>]. This is down to several factors, including the open nature of Android, the availability of Android-powered devices in every price bracket globally and the update model of Android. The update model in particular is likely a driving factor. iOS updates are downloaded by approximately half of users after one month of availability, Android updates can have uptake as low as 1% after one month [<a href="#3">3</a>]. Consequently, iOS has a smaller surface area to attack, while Android’s surface area increases as vulnerabilities go unpatched by users decisions to not update. 

This does not mean iOS is free from malicious apps. The notion that iOS is largely free of malware contributes to reduced security research for specific issues, including hidden illicit UI [<a href="#1">1</a>]. Research on illicit user interfaces is a smaller subset of security research and Android research outnumbers iOS research. Not until October 2019 did Lee et al study the issue, uncovering 142 illicit active apps.
 
<div style="text-align:center;"><img src="/images/posts/2021/hidden-illicit-ui-music-player-app.png" alt="View of a music player app with hidden UI paying users to download specific apps." style="width: auto;"/></div>

<p style="text-align: center; font-style: italic;">Figure 2: music player app with hidden crowdturfing UI.</p>

Figure 2 shows an example of an app which passed the App Store review process and implemented a fully functional music app while having a hidden UI enabling crowdturfing. Crowdturfing is an activity which allows users to make money by performing app downloads to boost their ranking on the App Store. The fully functional music app UI is shown on the left, and the illicit hidden UI on the right. A user who accesses the hidden UI can scroll through a list of apps to boost, with the reward value listed next to each.

Prior work on iOS had focused on privacy leaks[<a href="#6">6</a>], API abuses[<a href="#1">1</a>] or similar techniques which may have incidentally captured the behaviour of hidden and illicit UI in iOS. Lee et al analysed 28,000 applications available on the App Store, captured over 6 months in 2019 using a custom machine-learning tool called Chameleon-Hunter. Over the period Chameleon-Hunter discovered 142 applications conducting illicit activities while disguising the behaviour with a legitimate interface, leaving the activity hidden to the user. Having passed Apple’s vetting procedure the apps had gone on to conduct activities such as collecting users’ private information, defrauding users and promoting pirate app stores.

Apple are known to have a stringent vetting process, Lee et al pick out a recent example showing the App Stores security-first approach. Beyond banning apps which break their terms, Apple vets APIs, the services which provide application programmers with various functionalities. JSPatch was deemed a threat to the App Store and blocked. JSPatch allowed developers to use an API which could be used to update and alter code after review. The API had a dual-use; serving the legitimate purpose of fixing issues which are found after release, but with the potential to be used to circumnavigate App Store policies[<a href="#1">1</a>].

Lee et al provide breakdown of the activity of each of the 142 illicit apps:

<div style="text-align:center;"><img src="/images/posts/2021/lee-et-al-table-6.png" alt="." style="width: auto;"/></div>

<p style="text-align: center; font-style: italic;">Figure 3: breakdown of illicit app activity.</p>

<div style="text-align:center;"><img src="/images/posts/2021/lee-et-al-table-7.png" alt="." style="width: 80%;"/></div>

<p style="text-align: center; font-style: italic;">Figure 4: breakdown of illicit app App Store category.</p>

Most of the apps (65%) fall into the categories of Utilities, Music and Entertainment. The researchers point out anecdotal evidence that recorders and file manager apps are potential favourites among illicit app developers, likely due to the ease of creation and maintenance. 

The malicious apps found by Lee et al had significant exposure to users. Of the 142, 4 reached the top 20 leaderboards in various countries (the researchers cite China and Laos). At least 8 apps reached the top 50 and 14 the top 100 in their respective categories.

## References

<ol>
<li id="1">Lee, Y., Wag, X., Liao, X., and Wang, X. (2019) Understanding Illicit UI in iOS apps Through Hidden UI Analysis. <a href="https://ieeexplore.ieee.org/document/8888213" target="_blank">https://ieeexplore.ieee.org/document/8888213</a>.</li>

<li id="2">Fernandes, E., Chen, Q., Paupore, J., Halderman, A., Mao, Z., and Prakash, A. (2016) Android UI Deception Revisited: Attacks and Defenses. <a href="https://link.springer.com/chapter/10.1007/978-3-662-54970-4_3" target="_blank">https://link.springer.com/chapter/10.1007/978-3-662-54970-4_3</a>.</li>

<li id="3">F-Secure (2017) Another reason 99% of mobile malware targets androids. <a href="" target="https://blog.f-secure.com/another-reason-99-percent-of-mobile-malware-targets-androids">https://blog.f-secure.com/another-reason-99-percent-of-mobile-malware-targets-androids</a></li>

<li id="4">Kaspersky (2014a) Mobile Malware Evolution. <a href="https://securelist.com/mobile-malware-evolution-2019/96280/" target="_blank">https://securelist.com/mobile-malware-evolution-2019/96280/</a>.</li>

<li id="5">Kaspersky (2014b) Latest version of Svpeng targets users in US. <a href="https://securelist.com/latest-version-of-svpeng-targets-users-in-us/63746/" target="_blank">https://securelist.com/latest-version-of-svpeng-targets-users-in-us/63746/</a>.</li>

<li id="6">Deng, Z., Saltaformaggio, B., Zhang, X., and Xu, D. (2015) iRiS: Vetting Private API Abuse in iOS Applications. <a href="https://dl.acm.org/doi/10.1145/2810103.2813675" target="_blank">https://dl.acm.org/doi/10.1145/2810103.2813675</a></li>
</ol>
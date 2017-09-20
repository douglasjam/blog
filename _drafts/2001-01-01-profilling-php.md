---
layout: post
title: Profilling PHP with Blackfire
published: false
categories:
  - PHP
---
<ac:image ac:width="400"><ri:attachment ri:filename="blackfire-logo.png"></ri:attachment></ac:image>

## 1 - What is Blackfire

Blackfire is a tool to profile and measure and debug the code performance in order to improve it.

They basically rebuild xhprof getting rid of unecessary data and made an beautiful tool to analyze and compare it.

Read more about it here: [https://blackfire.io/docs/introduction](https://blackfire.io/docs/introduction)

## 2 - Registering 

2.1 - Go to [https://blackfire.io/signup](https://blackfire.io/signup) and sign up using a SensioLabs Account (use an mail instead social networks).

2.2 - Register an account using your **company mail <ac:link><ri:attachment ri:filename="Screen Shot 2016-09-27 at 17.51.33.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>**

2.3 - They will send you a email to active your account, after this you have a SensioLabs account

2.4 - Go back to [https://blackfire.io/login](https://blackfire.io/login) and login using your new account info

2.5 - Accept the terms

## 3 - Configuring locally

3.1 - Login into your blackfire.io account

3.2 - Click in the blue button Setup Environment <ac:link><ri:attachment ri:filename="screen-setup-env.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>

3.3 - Copy your server id, server token, client id and client token  <ac:link><ri:attachment ri:filename="screen-server-id.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link> <ac:link><ri:attachment ri:filename="screen-client-id.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>

3.4 - Add this information to your config.yml inside vagrant folder <ac:link><ri:attachment ri:filename="vagrant-config.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>

3.5 - Make a provision of your vagrant again (**vagrant up --provision**)

<ac:image ac:height="150" ac:thumbnail="true"><ri:attachment ri:filename="screen-client-id.png"></ri:attachment></ac:image><ac:image ac:height="150" ac:thumbnail="true"><ri:attachment ri:filename="screen-server-id.png"></ri:attachment></ac:image><ac:image ac:height="150" ac:thumbnail="true"><ri:attachment ri:filename="vagrant-config.png"></ri:attachment></ac:image>

## 4 - Activating profiler

4.1 - Access your vagrant

4.2 - Now we have two new commands **bon **and **boff**, this basically means blackfire on and blackfire off. In order to use the profiller you have to activate xdebug and blackfire, **bon** do both at once.

4.3 - From now all your calls to backend in AmfGateway will be sent blackfire overview at [https://blackfire.io/dashboard/mine/profiles](https://blackfire.io/dashboard/mine/profiles) <ac:link><ri:attachment ri:filename="blackfire-dashboard.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>

## 5 - Executing the profiler

You have two ways do perform this action:

5.1 - Manually via the game

*   Just open the game and do the action, e.g: place Building, immediately you will see the  **_CityMapService::placeBuilding_**_as the last or one of the lasts profiles in blackfire dashboard._

5.2 - Via functional tests <ac:emoticon ac:name="laugh"></ac:emoticon>

*   Basically you run one functional test that does one or more requests in the backend, the advantage from this is that the blackfire dashboard will be less poluted with unwanted requests that the client can made.

After the execution of the action, no matter how it will be listed in the dashboard, you just have to click in the bold link that references to your call, something like:

<ac:image ac:border="true" ac:height="64" ac:width="620"><ri:attachment ri:filename="blackfire-open-profile.png"></ri:attachment></ac:image>

[https://blackfire.io/docs/reference-guide/analyzing-profiles](https://blackfire.io/docs/reference-guide/analyzing-profiles)

## 6 - Understanding the profiled data

### 6.1 - The top bar

<ac:image ac:width="308"><ri:attachment ri:filename="blackfire-topbar.png"></ri:attachment></ac:image>

6.1.1 - Blackfire logo, clicking here you go to the dashboard with all profiles

6.1.2 - ServiceName::methodName, the profiled call title, hovering this you get more informations about the request

6.1.3 - Response time, how much time the request spend to be processed, clicking here you switch to **time oriented view**

6.1.4 - Memory consumed, how much memory the request spend to be processed, clicking here you switch to **memory oriented view**

### 6.2 - Functions tab

<ac:image ac:height="150" ac:thumbnail="true"><ri:attachment ri:filename="blackfire-functions.png"></ri:attachment></ac:image>

6.2.1 - The recommendations and assertions tab is only for premium users.

6.2.2 - The search input allows you to search for a method that was used in this request, after searching it allows you to get more data about it and also go do this function call in the callgraph

6.2.3 - _call table_.: It list all functions that were called at least once in this request 

6.2.3.1 - Column Function / Metric: basically list the functions called in the system, can be from some framework, php core or our functions.

6.2.3.2 - % Excl.: It means, how long take to execute this function **without** considering others functions called inside.

6.2.3.3 - % Incl.: How long take to execute this function **including **also the time to execute the functions call inside.

6.2.3.4 - Calls: How many times this function was called.

### **6.3 Detailing a call**

If you click in a method in the _call table_ you will get an expanded view, this gives you informations like:

6.3.1 - Function path, how may times was called (**Ig\StratCity\Classes\Models\CityMap::getMapEntities    6**)

6.3.2 - How many different functions called it **2 callers (6 calls)**

6.3.3 - How much time was spend on each call (you can see 2 buttons, first call you see that spend 95% in comparison with the other call (in the second we had it cached))

6.3.3.1 - Clicking in this button you see more details about who called it, also some metrics about this call

6.3.4 - The white block basically have:

6.3.4.1 - Function path

6.3.4.2 - Function name

6.3.4.3 - Inclusive time spend in this method call

6.3.4.4 - Memory spend in this call

6.3.4.5 - A magnifying glass: when you click you will be moved to this call in the callgraph

6.3.4.6 - Graphs that shows the time that this function spend considering all request

6.3.4.7 - Graphs that shows the memory that this function spend considering all request

6.3.5 - The last 3 orange/gray buttons bellow the white block means that internally on this functions the methods spend respectively 70%, 24% and 5%, where gray the orange ones you can click to get extra information and the gray one it the cost from the function itself.

<ac:image ac:height="250"><ri:attachment ri:filename="blackfire-detailing.png"></ri:attachment></ac:image>

### 6.3 - Callgraph

It is a graphical representation of the request stacktrace, where you can see the functions call order, time spend and others in a more ordered way.

6.3.1 - Looking from the vertical perspective you can see which function call which, per example, in the image below CityProduction::start calls CityProduction::doStart

6.3.2 - When it separate the calls horizontally, it means that both functions were called in the same function, where the order is from left to right, per example, in the image below: CityProductionService::startProduction called 

CityMap::getRefreshedCityMapEntityById and CityProduction::start.

6.3.3 - The pink bold arrows means the flow of the execution that was more expensive.

6.3.4 - The pink border in the rectangle nodes means how expensive was this function call in a general comparison with all others <ac:link><ri:attachment ri:filename="blackfire-callgraph-cost.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>

6.3.5 - You can also see a number above the rectangles (1x), it means how many times this function were called.

6.3.6 - You can see a magnifier when you hover some nodes, when you press it you focus and detail the graph based on this call ahead <ac:link><ri:attachment ri:filename="blackfire-detailing-call.png"><ac:plain-text-link-body></ac:plain-text-link-body></ri:attachment></ac:link>

6.3.7 - When you also click in a rectangle node, it will hover it in functions tab.

### <ac:image ac:height="250"><ri:attachment ri:filename="blackfire-callgraph-node.png"></ri:attachment></ac:image>

## 7 - Comparing two results

The main reason why you use a profiler is to speed up the code, and in order to speed up something you have to know the previous speed, to do this we have to do a comparison between two measures.

### 7.1 - Collecting profile samples

To do it, basically we have to execute the profiler twice, as explained in the step 5\. My recommendation is comparing between tags or a tag and your current version.

Below I show an example how to collect some samples of 2 different version in order to do a comparison.

<ac:structured-macro ac:macro-id="4384f72a-4034-44fd-bd50-6a80d209b622" ac:name="code" ac:schema-version="1"><ac:parameter ac:name="language">bash</ac:parameter> <ac:parameter ac:name="title">collecting samples</ac:parameter><ac:plain-text-body></ac:plain-text-body></ac:structured-macro>

### 7.2 - Picking the samples to compare

7.2.1 - After collecting some samples for the same request from 2 difference states, it is time to compare then, for this, go to blackfire.io dashboard.

There you will find all samples you collected, pick an average result for a branch/version and compare with the average result from other branch/version.

The best way is comparing the old result with the new one, so you will know if the performance decrease of increased, but you also can do in the other way around, or change afterwards.

To compare, click in compare from one sample and another.

<ac:image ac:height="150" ac:thumbnail="true"><ri:attachment ri:filename="blackfire-picking-comparasion.png"></ri:attachment></ac:image>

7.2.2 - After clicking in compare→to, you will be redirect to a page which compares both samples.

You will basically see the same view as callgraph and simple view, but the difference is that all will be in a relative mode, where it just says if it went faster or slower than the comparing sample.

In the example below, you can see that the execution went 5,89% slower and cost 0,741% memory.

You will also get different informations like how many more calls was made and different functions that were called.

Another difference is that instead of pink (cost call) we will see the color red (went slower) or blue (went faster)

<ac:image ac:height="150"><ri:attachment ri:filename="blackfire-comparison-view.png"></ri:attachment></ac:image> <ac:image ac:height="150" ac:thumbnail="true"><ri:attachment ri:filename="blackfire-comparison-red.png"></ri:attachment></ac:image><ac:image ac:height="150"><ri:attachment ri:filename="blackfire-comparison-blue.png"></ri:attachment></ac:image>

<span style="font-size: 20.0px;">8 - Tips & Warnings</span>

*   Using functional tests can simulate faster and isolated calls, but will not give you perfect simulation environment like, with cache created or a big city, depending on the case can be more suitable than a manual test, or not.
*   Blackfire requires his own extension enabled, that is an modified xhprofile, and with this enabled it decreases the performance considerable since they collect extra data from the calls. Then remember that the sample profiled will be different than the real result.

## 9 - Getting better into the tool

Please read the official Blackfire documentation in [https://blackfire.io/docs](https://blackfire.io/)

## 10 - Troubleshoot

10.1 - Profiler is not being executed or not going to the dashboard

*   Check your credentials if you filled the server and client id-token correctly, this can be found in config.yml inside vagrant folder.
*   Check if the branch you are have the blackfire sdk call in the AmfGateway, if is not present, checkout to develop, do a "ci" command to install the composer library, go to your desired branch and run cc (do not run ra, otherwise ci will be executed and remove blackfire sdk again)
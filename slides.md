<link rel="stylesheet" href="proj-css/talk.css">

<!--Cover Slide-->

[@purpleteamlabs](https://twitter.com/purpleteamlabs) <!-- .element: style="font-size: 5rem; color: #9b6bcc" target="_blank" -->

[@binarymistbooks](https://twitter.com/binarymistbooks) <!-- .element: style="font-size: 5rem; color: #9b6bcc" target="_blank" -->

[@binarymist](https://twitter.com/binarymist) <!-- .element: style="font-size: 5rem; color: #9b6bcc" target="_blank" -->

----  ----

<!--Intro Slide-->

# OWASP Meetup Covid

Note:

----

# Impacts

* What negative infosec impacts has Covid had on you and your work-place?
* What positive infosec impacts has Covid had on you and your work-place?

Note:

----

# Attackers Tactics

* What sort of attacks are on the rise?
  * Obviously phishing, what else?
* What have you and/or your org done or are doing about this?

Note:

----

# Business Continuity

* Has business continuity been affected for you, if so, how?
* How can you improve this?

* What do we need to be thinking about in our jobs in relation to InfoSec and personal OpSec?
* What must orgs and us personally be considering in order to sustain/create data, application, infrastructure and personal security while still considering efficiencies and user experience?

Note:

----

# Remote Work

* How has/is remote work changed/changing the infosec stack?
* What do we need to be thinking more about now than we used do?

* How do we educate staff on how to stay secure WFH?
* Only 38% of businesses have a cybersecurity policy in place. Is this OK, if not how to we improve this stat?

Note:

----

# Take-aways (Improvements)

* What do we need to improve?
* Ideas on how?

Note:

----




<!-- .slide: data-transition="none" -->
<!-- .slide: style="text-align:left" -->

`local` <!-- .element: style="font-size:3rem" -->

1. <!-- .element: class="fragment fade-right" --> <a href="https://doc.purpleteam-labs.com/local/local-setup.html" target="_blank">doc.purpleteam-labs.com</a>
2. <!-- .element: class="fragment fade-right" --> <a href="https://github.com/purpleteam-labs/purpleteam-lambda" target="_blank">Lambda functions</a>
3. <!-- .element: class="fragment fade-right" --> <a href="https://github.com/purpleteam-labs/purpleteam-s2-containers" target="_blank">Stage Two containers</a>
4. <!-- .element: class="fragment fade-right" --> <a href="https://github.com/purpleteam-labs/purpleteam-orchestrator" target="_blank">Orchestrator</a>
5. <!-- .element: class="fragment fade-right" --> <a href="https://github.com/purpleteam-labs/purpleteam-app-scanner" target="_blank">Testers</a>
6. <!-- .element: class="fragment fade-right" --> <a href="https://github.com/purpleteam-labs/purpleteam" target="_blank">purpleteam (CLI)</a>
7. <!-- .element: class="fragment fade-right" --> Run your <a href="https://github.com/purpleteam-labs/purpleteam-iac-sut" target="_blank">SUT</a>
8. <!-- .element: class="fragment fade-right" --> <code>purpleteam test</code>

<br><br>

Note:
* There's quite a bit of set-up to do
* You need to set-up all the mirco-services

1. All the set-up should be documented here.  
  Doc moving to proper docs site soon
2. Lambda functions
3. Stage 2 containers
4. orchestrator
5. Testers (only app currently)
6. CLI - get it on your system - git clone or npm install
  1. Configure it. Discussed soon, needs to be done for `cloud` env also
  2. Create _Job_ file. Also discussed soon
7. Run your SUT
8. Run the CLI

----

<!-- .slide: data-transition="none" -->
<!-- .slide: style="text-align:left" -->

`cloud` <!-- .element: style="font-size:3rem" -->

<br><br>

<ol>
  <li class="fragment fade-right">Infrastructure set-up for you</li>
  <li class="fragment fade-right">Get the CLI on your system <br><code class="fragment">git clone</code> <span class="fragment">or</span> <code class="fragment">npm install</code></li>
</ol>

<br><br><br><br>

Note:
1. All infrastructure set-up is done for you
2. Get the CLI on your system

----

<!-- .slide: data-transition="none" -->
<!-- .slide: style="text-align:left" -->

`cloud` <!-- .element: style="font-size:3rem" -->

<!-- .element: style="text-align:left" --> 3. Apply details to your CLI <a href="https://github.com/purpleteam-labs/purpleteam#configuration" target="_blank">config</a>

`config.cloud.json` <!-- .element: style="font-size:2rem" -->

```json [7|15|16|24|25|26|29|32]
{
  "loggers": {
    "def": {
      "level": "debug"
    },
    "testerProgress": {
      "dirname": "/path/to/your/purpleteam/cli_logs/"
    }
  },
  "purpleteamApi": {
    "protocol": "https",
    "host": "api.purpleteam-labs.com",
    "port": 443,
    "stage": "alpha",
    "customerId": "0",
    "apiKey": "aTcnpRX35vDbtLiXxGHlAeEWMGXhFk"
  },
  "testerFeedbackComms": {
    "medium": "lp"
  },
  "purpleteamAuth": {
    "protocol": "https",
    "host": "auth.purpleteam-labs.com",
    "appClientId": "8yIs8sjr8TDTbseZSlxSFKE9EvXu3l",
    "appClientSecret": "4ecl0j8gvlh50k8udk2emqegn64ogeh2nh5163joubtck1dsnsfGBZIEmMlsW",
    "custnSubdomain": "cust0"
  },
  "buildUserConfig": {
    "fileUri": "./testResources/jobs/dev/job_0.1.0-alpha.1_cloud"
  },
  "outcomes": {
    "dir": "/path/to/your/purpleteam/outcomes_transfered_to_cli/"
  }
}
```

Note:
Add your details to the CLI config
* testerProgress dirname

1. customerId
2. apiKey
3. appClientId
4. appClientSecret
5. custnSubdomain
6. Job file path
7. outcomes dir

----

<!-- .slide: data-transition="none" -->
<!-- .slide: style="text-align:left" -->

`cloud` <!-- .element: style="font-size:3rem" -->

<br>

4. Create _Job_ file

<br>

```json []
{
  "data": {
    "type": "testRun",
    "attributes": {
      "version": "0.1.0-alpha.1",
      "sutAuthentication": {
        "route": "/login",
        "usernameFieldLocater": "userName",
        "passwordFieldLocater": "password",
        "submit": "btn btn-danger",
        "expectedPageSourceSuccess": "Log Out"
      },
      "sutIp": "nodegoat.sut.purpleteam-labs.com",
      "sutPort": 443,
      "sutProtocol": "https",
      "browser": "firefox",
      "loggedInIndicator": "<p>Found. Redirecting to <a href=\"\/dashboard\">\/dashboard<\/a><\/p>",
      "reportFormats": ["html", "json", "md"]
    },
    "relationships": {
      "data": [{
        "type": "testSession",
        "id": "lowPrivUser"
      },
      {
        "type": "testSession",
        "id": "adminUser"
      }]
    }
  },
  "included": [
    {
      "type": "testSession",
      "id": "lowPrivUser",
      "attributes": {
        "username": "user1",
        "password": "User1_123",
        "aScannerAttackStrength": "HIGH",
        "aScannerAlertThreshold": "LOW",
        "alertThreshold": 12
      },
      "relationships": {
        "data": [{
          "type": "route",
          "id": "/profile"
        }]
      }
    },
    {
      "type": "testSession",
      "id": "adminUser",
      "attributes": {
        "username": "admin",
        "password": "Admin_123"
      },
      "relationships": {
        "data": [{
          "type": "route",
          "id": "/memos"
        },
        {
          "type": "route",
          "id": "/profile"
        }]
      }
    },
    {
      "type": "route",
      "id": "/profile",
      "attributes": {
        "attackFields": [
          {"name": "firstName", "value": "PurpleJohn", "visible": true},
          {"name": "lastName", "value": "PurpleDoe", "visible": true},
          {"name": "ssn", "value": "PurpleSSN", "visible": true},
          {"name": "dob", "value": "12235678", "visible": true},
          {"name": "bankAcc", "value": "PurpleBankAcc", "visible": true},
          {"name": "bankRouting", "value": "0198212#", "visible": true},
          {"name": "address", "value": "PurpleAddress", "visible": true},
          {"name": "website", "value": "https://purpleteam-labs.com", "visible": true},
          {"name": "_csrf", "value": ""},
          {"name": "submit", "value": ""}
        ],
        "method": "POST",
        "submit": "submit"
      }
    },
    {
      "type": "route",
      "id": "/memos",
      "attributes": {
        "attackFields": [
          {"name": "memo", "value": "PurpleMemo", "visible": true}
        ],
        "method": "POST",
        "submit": "btn btn-primary"
      }
    }
  ]
}
```

Note:
* Create a _Job_ file
* We've got a bunch of examples

----

<!-- .slide: data-transition="none" -->
<!-- .slide: style="text-align:left" -->

`cloud` <!-- .element: style="font-size:3rem" -->

<br><br>

5. Run your SUT
6. <!-- .element: class="fragment fade-right" --> <code>purpleteam test</code>

<br><br><br><br><br>

Note:
* Run your SUT

1. Run the purpleteam CLI
  * Inspect outcomes on completion

----  ----

## Architecture & Tech

Note:
10 minutes

----

<!-- .slide: data-transition="none" -->

<div style="text-align:left;font-size:3rem"><code>local</code></div>

![purpleteam](proj-img/purpleteam_local_2021-01-min.png)

Note:
* Orchestrator organises & supervisors the testers
* Discuss Redis pub/sub, lists, SSE and LP
* Discuss how the micro-services hang together and communicate with each other.
* Discuss sam cli hosts our lambda functions locally
* docker-compose-ui required to start/stop containers from within the tester containers
* testers run their lambdas, lambdas tell docker-compose-ui to spin up and tear down n stage 2 containers

----

<!-- .slide: data-transition="none" -->
<!-- .slide: style="text-align:left" -->

`cloud` <!-- .element: style="font-size:3rem" -->

<br>

Terraform - Terragrunt

<br>

1. <!-- .element: class="fragment fade-right" style="text-align:left" --> <b>static</b>
2. <!-- .element: class="fragment fade-right" style="text-align:left" --> <b>nw</b>
3. <!-- .element: class="fragment fade-right" style="text-align:left" --> <b>apiAuth</b>
4. <!-- .element: class="fragment fade-right" style="text-align:left" --> <b>contOrc</b>
5. <!-- .element: class="fragment fade-right" style="text-align:left" --> <b>api</b>

Note:
1. <b>static</b> (IAM roles, policies, ECR repository creation)
2. <b>nw</b> (network, VPC, load balancer, auth and api certificates, auth subdomain)
3. <b>apiAuth</b> (Cognito user pools, customer specific auth subdomain)
4. <b>contOrc</b> (SSH pub keys, EC2, Cloudwatch log groups, ECS, autoscaling, Lambdas)
5. <b>api</b> (API Gateway, Cloudwatch log groups, VpcLink, apis, api subdomain, usage plans, api keys)

----

<!-- .slide: data-transition="none" -->

<div style="text-align:left;font-size:3rem"><code>cloud</code></div>

![purpleteam](proj-img/purpleteam_cloud_2021-01-min.png)

Note:
* Orchestrator organises & supervisors the testers
* Discuss Redis pub/sub, lists, LP. Streaming APIs not supported in API Gateway
* Could use API Gateway WebSockets for bi-directional comms, but that doesn't support OAuth client-credentials flow
* Discuss the authn flow and everything else
  * CLI makes POST request to purpleteam auth domain with:
    * `grant_type`, `client_id` of the user pool app client, `scope`, `client_secret`
  * Cognito Authorisation server returns an `access_token`
  * App makes requests with `access_token` to the resource server which in our case is the API Gateway
  * Resource server/API Gateway validates the `access_token` with the User pool
* testers run their lambdas, lambdas tell ECS to spin up and tear down n stage 2 containers
* Origonally used ALB but that didn't support our authentication requirements, so had to back out and swap for API Gateway and NLB

----  ----

## Pressures

Note:
20 minutes

----

### Keeping NodeJS Dedendencies up to date

The <a href="https://github.com/purpleteam-labs/purpleteam/issues/29" target="_blank">last update</a> after doing the IaC

Note:
Discuss the never ending battle of keeping NodeJS dependencies up to date

----

### Forking/adopting libraries when maintainers disappear

Note:
Discuss Forking/adopting when maintainers lose interest

* docker-compose-ui
* mocksse
* Cucumber took some functionality away that we depend on
* others

----

### Keeping relationships alive

Note:
Keeping relationships alive

* Wife comes first...
* and that's about all the time I have
* I've had very little time for running OWASP Chch, InfoSecNZ or communicating on any other mediums
* Now that we're at alpha that's changing though 

----

<!-- .slide: style="text-align:left" -->

### Keeping yourself alive

* Nutrition
* Sleep
* Fitness

Note:
* Eating right
* Getting enough quality sleep
* Fitness, I spend 2 hours at the gym 6 days a week. Health would plummet otherwise

----

<!-- .slide: style="text-align:left" -->

### Competitors

When I started purpleteam

<ul>
  <li class="fragment strike" data-fragment-index="1">BDD-Security</li>
</ul>

<span class="fragment" data-fragment-index="1">Now...</span>

<ul>
  <li class="fragment">StackHalk</li>
  <!-- <li class="fragment">GuardRails</li> -->
  <li class="fragment">Gitlab</li>
</ul>

<span class="fragment">purpleteam is standalone</span><span class="fragment">, only does one thing<span>

Note:
BDD-Security

1. seems to have gone away
2. StackHalk (recruited Simon Bennets)
3. ~~Guard Rails just starting DAST. Talk about them hiring me~~
4. Gitlab has a DAST component on ultimate

----

### Shout Outs

* Craig Rowland &nbsp;&nbsp; @SandflySecurity
* Simon Bennetts @psiinon
* Ricardo &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; @thc202
* Leanne Carter &nbsp;&nbsp;&nbsp; @nzquail
* Akshath Kothari @ricekot

Note:
* Craig Rowland &nbsp;&nbsp;&nbsp; (Sandfly Security)
* Simon Bennetts &nbsp; (OWASP Zap)
* Ricardo &nbsp;&nbsp;&nbsp; @thc202
* Leanne Carter &nbsp;&nbsp;&nbsp; (my rock)
* Akshath Kothari     Helping with engineering purpleteam

----  ----

# Next Steps?

* <!-- .element: class="fragment fade-right" style="text-align:left" --> purpleteam <code>local</code> is now an <a href="https://owasp.org/www-project-purpleteam/" target="_blank">OWASP project</a>

Note:
23 minutes

1. purpleteam `local` is now an OWASP project

----

## Consuming purpleteam


Note:
* How can you start using it today?
* As discussed in the Environments section:
  * `local`: set everything up yourself
  * `cloud`: Sign-up for an account, set-up your test Job, get the CLI on your system

----

## Contributing to purpleteam

* <a href="https://github.com/purpleteam-labs/purpleteam/discussions" target="_blank">Github Discussions</a>
* <a href="https://owasp.slack.com/messages/project-purpleteam" target="_blank">OWASP purpleteam Slack</a>
* <a href="https://github.com/purpleteam-labs/purpleteam/projects/2" target="_blank">Project Board</a>
* <a href="https://github.com/purpleteam-labs/purpleteam/issues" target="_blank">Submit Issue</a>
* <a href="https://github.com/purpleteam-labs/purpleteam/pulls" target="_blank">Submit PR</a>
* <a href="https://github.com/purpleteam-labs/purpleteam/security/policy" target="_blank">Reporting Security Issues</a>
* <a href="https://github.com/purpleteam-labs/purpleteam/projects/1" target="_blank">Public Roadmap</a>
* <a href="https://github.com/purpleteam-labs/purpleteam/blob/main/CONTRIBUTING.md" target="_blank">CONTRIBUTING.md</a>

Note:
* If it's missing something you need or you find a bug
* Adding different testers

----

## purpleteam Next Steps

* Docs site
* Landing page
* Help Dev Teams to start using purpleteam
* Development

Note:
* Proper docs site
* Proper landing page
* If you have a Dev Team that is keen to try purpleteam out, talk to me after
* We're always looking for people to work on the codebase. Even if you're a student, it's a great way to learn about security, by coding it

----

purpleteam-labs.com <!-- .element: style="font-size: 5rem;" -->



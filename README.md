# amplify-cognito-trigger-sample
Sample repo to reproduce amplify Cognito triggers detaching behaviour

I have replicated the issue in amplify version `6.3.1` & `7.4.4` in respective branches : `amplify-v6.3.1` | `amplify-v7.4.4`

Steps to reproduce on version `7.4.4`:
-----
```bash
# install amplify, current latest is 7.4.4
npm install -g @aws-amplify/cli
# init project with default setting
amplify init
# configure auth with cognito at least one trigger -- equivalent to commit a3ed91fb86479f3e26871ba95af05e0372fe9dab
amplify add auth
# deploy
amplify push

# all good at this point, triggers are attached.

# update cognito password policy
amplify auth update
# deploy
amplify push

# password policy gets updated and existing triggers are now detached from cognito :(
```

Consistent with amplify versions 5, 6 & 7

It's clear that the approach for attaching triggers to cognito is through a lambda function trigger.
From logs I cannot see an invocation after update here in this new version but old version used to get a delete which was causing similar trouble.
But in all cases triggers gets detached automatically after any updates to cognito.

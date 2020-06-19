---
layout: post
title:  "Auth Feedback"
date:  2020-04-26 21:43:54 +1300
categories: jekyll update
---

### Meetings

This week since Polytech classes were running again we started having meetings with David on Mondays and Thursdays at 1:30 to show new features and discussed what we should work on until our nest meeting. Tren, Liam and I would then always have a separate meeting afterwards like we were doing in the holidays to keep track of progress, discuss issues and distribute work.

# Login/Sign-up Feedback


One of the bigger issues I was tasked with was providing feedback to the user when they provide incorrect details when they login or sign-up.

First I had to make sure that the errors that were being returned by the site were human readable. Most were except fo the confirm password field. If the confirm password field was entered incorrectly the site would return
```
'confirmPassword' must be [ref:password]
```
which shouldnt be shown to the user. So in the signup schema I added:
```
  confirmPassword: Joi.valid(Joi.ref('password'))
  .required()
  .messages({
    "any.only": 'Confirm Password must match Password',
    "any.required": 'Confirm Password is required'
  }),
```
which overwrites the errors that are being stored into state with a custom message. any.only means only certain values were allowed, but the input didn't match any of them.

states
useSelector
further understanding of site as a whole

At this point I was getting more comfortable using states and useSelectors to get/store information. And was more experienced with material ui so I knew that material ui text fields had the ability to attach errors.
```
 <TextField
    name="name"
    ...
    error={nameHasError}
    helperText={nameHelperText}
```

I also had to edit the error state duck to return the errors after a login/signup attempt. An example of one:
```
export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    case POST_SIGNUP_SUCCESS:
      return { ...state, loading: false, errors: [] };
```

I also had to add and edit some functions in the users saga to create and get the errors:
```
function createGeneralError(errorMessage) {
  return { type: ['general'], message: errorMessage };
}

function getErrorsFromResponse(response) {
  return response.data.errors
    ? response.data.errors
    : [createGeneralError(response.statusText)];
}
```
A full list changes can be found in this pull request: 
<https://github.com/op-analytics/NYT-Media-Analytics/pull/268>
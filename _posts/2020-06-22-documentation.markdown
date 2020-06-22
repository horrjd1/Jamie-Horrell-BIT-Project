---
layout: post
title:  "Week 16 - Final"
date:   2020-06-18 19:53:46 +1300
categories: jekyll update
---

# Documentation

I spent parts of the weekend aswell as today (Monday) helping complete the projects documentation with Trent and Liam.


## API Documentation
[Commit here.](https://github.com/op-analytics/Media-Analytics/pull/396/commits/4d02173ac929875c32a1d56d09706e7fbfaef856) This is the swagger api documentation we made. Swagger takes this specially formatted json file and uses it to generate a web page. Screenshots of the finished api documentation page:

![alt text](/Jamie-Horrell-BIT-Project/images/swagger-api-doc-1.PNG)
![alt text](/Jamie-Horrell-BIT-Project/images/swagger-api-doc-2.PNG)

## Back-End Documentation
[Pull request here](https://github.com/op-analytics/Media-Analytics/pull/406) showing all back-end documentation/commenting. To document the back end we added header comments to every method and added comments to sections of code that arent very self explanatory. Heres an example of a documented method:
```
/**
 * Login a user (Get the jwt access token)
 *
 * @param req - Express' request object
 * @param res - Express' response object
 */
export async function login(req: Request, res: Response): Promise<void> {
  const { email: emailDirty, password } = req.body;
  const email = emailDirty.toLowerCase();

  // Try get user with the given email
  const user = await GetUser(email);

  // When no matching user was found or when the passwords dont match
  if (!user || !(await PasswordsMatch(password, user.password))) {
    res
      .status(400)
      .json({ errors: [createValidationError('Incorrect information')] });
    return;
  }

  // If email was already confirmed
  if (!user.confirmed) {
    res.status(400).json({
      errors: [createValidationError('Email has not yet been validated')],
    });
    return;
  }

  // Return an access token containing safe user information
  res.json({ token: TokenizeUser(user) });
}
```

## Wiki
We continued to update the wiki page to reflect the current state of the project. Heres some of the pages I updated:
- <https://github.com/op-analytics/NYT-Media-Analytics/wiki/Issues>
- <https://github.com/op-analytics/NYT-Media-Analytics/wiki/Folder-Structure>
- <https://github.com/op-analytics/Media-Analytics/wiki>


Heres an example of wiki documentation i wrote:
```
## Issue Templates
We have set up multiple templates that are available for contributors to use when they open new issues. You will be required to select one when you create a new issue. The templates we have made include:

### Bug Report
Create a report on a bug found on the site. Should provide details such as a description of the bug, the steps taken to produce the bug, screenshots, device and OS.

### Improvement/Suggestion
An improvement or a suggestion that may make the project better.

### Task
An issue created by developers describing a feature or problem that needs to be worked on.

### User Story
An issue/feature request made by a user or from the perspective of a user. Should be in the format "As a [ type of user ], I want [ some goal ] so that [ some reason ]".
```

#### Resources
I made an effort to find beginner friendly tutorials and resources to help students coming into this project as I struggled myself at the beginning with learning the large amount of new languages and technologies. heres a [link](https://github.com/op-analytics/Media-Analytics/pull/406) to that wiki page I created. I made sure these tutorials were relevant to the methodologies we're using in the project.
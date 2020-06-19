---
layout: post
title:  "Week 3"
date:   2020-03-07 19:32:51 +1300
categories: jekyll update
---

# Week 3

I had been tasked with removing the Topic Modelling and Sentiment Analysis sections from the site as they either weren’t completed (made by students from the previous semester who have since left) or aren’t working correctly/up to standard. This required me to know/understand the basic structure of the project in order to find what to remove as well as the knowledge on how ReactJS handle routes. I did this with Liams supervision just to make sure that what I was doing was correct.

It was also at this point that I was taught more about how they tested their project before making pull requests by using the commands
```
- Npm I -D
- Npm run tests
```

This did result in a error with my fix for the graphs so this allowed me to fix the issue before the pull request got made.

# Test

On the second lesson Trent and Liam got me to write a test for the user authentication they had just finished. Which was great as, though im unable to write code to for a authentication system for the site at this stage, it allowed me to go through what they've done and understand it. Heres the test that I wrote in express-back-end/test/auth/routes.spec.js:
```
describe('GET /user', () => {
  let token;
  let user;
  before(async () => {
    createDB();
    const UserData = {
      name: 'Bob',
      email: 'bob@builder.com',
      password: 'Yes@WeCan',
    };
    // Hash the password
    const salt = await bcrypt.genSalt(10);
    const hashedPassword = await bcrypt.hash(UserData.password, salt);

    // Try save and tokenize the user return error if it doesn't work
    user = new User({
      ...UserData,
      password: hashedPassword,
    });
    await user.save();

    const res = await request(app)
      .post('/api/auth/login')
      .send({ email: 'bob@builder.com', password: 'Yes@WeCan' })
      .expect(200);
    token = res.body.token;
  });

  it('It should return the user that the token on the request belongs to', async () => {
    const res = await request(app)
      .get('/api/auth/user')
      .set({ Authorization: token })
      .expect(200);
    expect(res.body.data).to.be.an('object');
    expect(res.body.data.name).to.equal('Bob');
    expect(res.body.data.email).to.equal('bob@builder.com');
  });

  it('It should return UnAuthorized when called with an invalid token', async () => {
    const res = await request(app)
      .get('/api/auth/user')
      .set({ Authorization: 'fake_token' })
      .expect(401);
    expect(res.body.message).to.be.an('string');
    expect(res.body.message).to.equal('UnAuthorized');
  });

  after(() => {
    destroyDB();
  });
});
```
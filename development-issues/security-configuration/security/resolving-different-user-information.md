# Resolving different user information

There is two kinds of user information that security middleware is need. First is how to get user from the system schema. Second how to determine what information it can access.

Look to `api4/src/app.ts`

```javascript
[...]
 passport.init(app, passportLib, resolveUser);
[...]
 app.use(middleware.ownerDiscovery(resolveOwner));
[...]
```

The two library methods `resolveUser` and `resolveOwner` is responsible for getting those two kind of information from the system.


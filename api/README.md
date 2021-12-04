# Woolgens-api docs

## Table of contents
- [ Constants ](#constants)
- [ User data ](#user-data)

<a name="constants"></a>
## Constants

```java
WoolgensConstants.PREFIX
```

<a name="user-data"></a>
## User data

### Retrieve user:

```java
UserProvider<User> provider = WoolgensApi.getProvider(UserProvider.class);
User user = provider.getUserByUUID(player.getUniqued());
provider.saveAsync(user, true);
```

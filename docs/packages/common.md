# @foal/common

`@foal/common` consists of several hooks, controller factories and services that are generally used in an project.

## Post-hooks

### `afterThatLog(message: string, logFn = console.log)`

Logs the message with the given log function (default is console.log).

Example:
```typescript
@Service()
@afterThatLog('A method has been called!')
class Service {}
```

### `afterThatRemoveField(name: string)`

Removes the given field from the context result. If the context result is an array, it removes the field from each of its items.

Example:
```typescript
@Service()
class UserService {

  @afterThatRemoveField('password')
  public getUser() {
    return { username: 'foobar', password: 'my_crypted_password' };
  }

  @afterThatRemoveField('password')
  public getUsers() {
    return [
      { username: 'foobar', password: 'my_crypted_password' },
      { username: 'barfoo', password: 'my_other_crypted_password' }
    ];
  }
}
```

## Pre-hooks

### `log(message: string, logFn = console.log)`

Logs the message with the given log function (default is console.log).

Example:
```typescript
@Service()
@log('A method has been called!')
class Service {}
```

### `methodNotAllowed()`

Throws a MethodNotAllowedError. The client gets a `405 Method Not Allowed`.

```typescript
@Service()
class OrganizationService {

  @methodNotAllowed()
  public delete(id) {
    // Deletes the org.
  }
}
```

### `restrictAccessToAuthenticated()`

Returns a 401 status if the user is not authenticated.

### `restrictAccessToAdmin()`

Returns a 401 status if the user is not authenticated and a 403 if `ctx.user.isAdmin` is not truthy.
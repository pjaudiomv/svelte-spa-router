# Migration Guide: Svelte 4 to Svelte 5

This guide will help you migrate your svelte-spa-router usage from Svelte 4 to Svelte 5.

## Event Handling Changes

The main breaking change in Svelte 5 is how events are handled. Instead of using `on:` directives, events are now passed as props with the `on` prefix.

### Before (Svelte 4)

```svelte
<Router 
  {routes}
  on:routeLoading={handleRouteLoading}
  on:routeLoaded={handleRouteLoaded}
  on:conditionsFailed={handleConditionsFailed}
/>
```

### After (Svelte 5)

```svelte
<Router 
  {routes}
  onrouteLoading={handleRouteLoading}
  onrouteLoaded={handleRouteLoaded}
  onconditionsFailed={handleConditionsFailed}
/>
```

## Removed Features

### `routeEvent` 

The `routeEvent` mechanism for bubbling events from child components has been removed, as Svelte 5 no longer supports automatic event forwarding. 

**Alternative solutions:**
- Use callback props explicitly
- Use Svelte stores for state management
- Use Svelte context API for component communication

### Before (Svelte 4)

```svelte
<!-- Parent component -->
<Router {routes} on:routeEvent={handleRouteEvent} />

<!-- Child component -->
<button on:click={() => dispatch('routeEvent', {foo: 'bar'})}>
  Click me
</button>
```

### After (Svelte 5)

Use callback props instead:

```svelte
<!-- Parent component -->
<Router {routes} />

<!-- Pass callbacks to child components via route props or stores -->
```

## What Stays the Same

The following features continue to work without changes:

- Route definitions
- Dynamic imports with `wrap`
- Pre-conditions
- Static props
- Stores (`$location`, `$querystring`, `$params`)
- Navigation functions (`push`, `pop`, `replace`)
- `link` action
- Nested routers

## Summary

The migration is minimal - you only need to:
1. Update event handler syntax from `on:eventName` to `oneventName`
2. Remove any usage of `routeEvent` and replace with explicit callbacks or stores
3. Update your `package.json` to use Svelte 5

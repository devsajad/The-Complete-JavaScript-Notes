## Local Storage API

### Introduction

- Local storage allows us to persist data across page reloads.
- It is a key-value storage system provided by the browser.

### Key Concepts

- Data stored in local storage remains even after closing the browser or refreshing the page.
- Local storage is linked to the URL of the application.

### Basic Operations

1. **Storing Data**

   - When a new workout is added, store the workouts array in local storage.

   ```javascript
   localStorage.setItem("workouts", JSON.stringify(this.workouts));
   ```

2. **Retrieving Data**

   - On page load, retrieve data from local storage.

   ```javascript
   const workoutsData = JSON.parse(localStorage.getItem("workouts"));
   ```

3. **Removing Data**

   - To remove data from local storage, you can use the `removeItem` method. This method takes a key as its parameter and removes the corresponding entry from storage.

   ```javascript
   localStorage.removeItem("workouts");
   ```

You can also clear all data in local storage using the `clear` method:

```javascript
localStorage.clear();
```

## Reloading a Page with the Location Object

To reload the current page using the `location` object, you can use the `location.reload()` method. This can be particularly useful if you want to refresh the page after making changes to the data displayed.

### Example:

```javascript
location.reload();
```

## The Problem: Losing the Prototype Chain

When you store objects in local storage, they are serialized to strings using `JSON.stringify()`. When you retrieve them, you use `JSON.parse()` to convert them back to objects. However, this process does not retain the prototype chain of the original objects.

### Explanation:

1. **Serialization**: When an object is serialized, its methods and prototype information are not included.
   ```javascript
   const workout = new Workout(); // Workout is a class
   const workoutString = JSON.stringify(workout); // Just a plain string
   ```
2. **Deserialization**: When you parse the string back to an object, it becomes a plain object without the original class methods.

   ```javascript
   const parsedWorkout = JSON.parse(workoutString); // This is a plain object
   ```

3. **Loss of Methods**: As a result, any methods that were defined in the original class (like `workout.click`) are no longer available on the parsed object.
   ```javascript
   parsedWorkout.click(); // TypeError: parsedWorkout.click is not a function
   ```

### Solution:

To maintain the prototype chain, you can manually re-instantiate the objects after retrieving them from local storage:

```javascript
const workoutsData = JSON.parse(localStorage.getItem("workouts"));
this.workouts = workoutsData.map((data) => new Workout(data)); // Recreate instances
```

By doing this, you ensure that the objects retain their methods and can function as intended.

### Important Considerations

- Local storage is suitable for small amounts of data due to its blocking nature.
- Avoid using local storage for large datasets to prevent performance issues.

### Conclusion

- Local storage is a simple and effective way to maintain state across page sessions in web applications.

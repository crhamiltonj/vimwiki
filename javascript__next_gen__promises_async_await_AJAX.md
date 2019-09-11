# Promises / Async Await / AJAX

## Asynchronous Code

```javascript
const second = () => {
  setTimeout(() => {
    console.log("Async Hey There!");
  }, 2000);
};

const first = () => {
  console.log("Hey There!");
  second();
  console.log("The End!");
};
```

## Asynchronous Javascript with Callbacks

```javascript
function getRecipe() {
  setTimeout(() => {
    const recipeID = [523, 883, 432, 974];
    console.log(recipeID);
    setTimeout(
      id => {
        const recipe = { title: "Fresh tomato pasta", publisher: "Jonas" };
        console.log(`${id}: ${recipe.title}`);
        setTimeout(
          publisher => {
            const recipe = { title: "Italian Pizza", publisher: "Jonas" };
          },
          1500,
          recipe.publisher
        );
      },
      1000,
      recipeID[2]
    );
  }, 1500);
}
getRecipe();
```

## Promises

A Promise

- is an object that keeps track of whether a certain event has happened already or not
- determines what happens after the event has happened
- implements the concept of a future value that we're expecting

### Promise states

- Pending - the state before an evemt happens
- Settled / Resolved - The state after the event happens which could be

  - Fulfilled - the event completed successfully
  - Rejected - The event failed

```javascript
const getIDs = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve([523, 883, 432, 974]);
  }, 1500);
});

const getRecipe = recID => {
  return new Promise((resolve, reject) => {
    setTimeout(
      ID => {
        const recipe = { title: "Fresh tomato pasta", publisher: "Jonas" };
        resolve(`${ID}: ${recipe.title}`);
      },
      1500,
      recID
    );
  });
};

const getRelated = publisher => {
  return new Promise((resolve, reject) => {
    setTimeout(
      pub => {
        const recipe = { title: "Italian Pizza", publisher: "Jonas" };
        resolve(r`${pub}: ${recipe.title}`);
      },
      1500,
      publisher
    );
  });
};

getIDs
  .then(IDs => {
    console.log(IDs);
  })
  .then(recipe => {
    console.log(recipe);
    return getRelated("Jonas");
  })
  .then(recipe => {
    console.log(recipe);
  })
  .catch(error => {
    console.log("Error!!");
  });
```

## Async / Await

```javascript
const getIDs = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve([523, 883, 432, 974]);
  }, 1500);
});

const getRecipe = recID => {
  return new Promise((resolve, reject) => {
    setTimeout(
      ID => {
        const recipe = { title: "Fresh tomato pasta", publisher: "Jonas" };
        resolve(`${ID}: ${recipe.title}`);
      },
      1500,
      recID
    );
  });
};

const getRelated = publisher => {
  return new Promise((resolve, reject) => {
    setTimeout(
      pub => {
        const recipe = { title: "Italian Pizza", publisher: "Jonas" };
        resolve(r`${pub}: ${recipe.title}`);
      },
      1500,
      publisher
    );
  });
};

async function getRecipesAW() {
  const IDs = await getIDs;
  console.log(IDs);
  const recipe = await getRecipe(IDs[2]);
  console.log(recipe);
  const related = await getRelated("Jonas");
  console.log(related);

  return recipe;
}

const rec = getRecipesAW().then(result =>
  console.log(`${result} is the best ever.`)
);
```

## AJAX and APIs

### Making API calls with fetch and Promises

```javascript
fetch("https://crossorigin.me/https://www.metaweather.com/api/location/2487956")
  .then(result => {
    console.log(result);
  })
  .catch(error => console.log(error));
```

### Making API calls with Async / Await

```javascript
async function getWeatherAW(woeid) {
  try {
    const result = await fetch(
      "https://crossorigin.me/https://www.metaweather.com/api/location/2487956"
    );
    const data = await result.json();
    console.log(data);
    return data;
  } catch (error) {
    alert(error);
  }
}

getWeatherAW(2487956);
let dataLondon;
getWeatherAW(44418).then(data => {
  dataLondon = data;
  console.log(dataLondon);
});
```

[Back](javascript__next_gen.md)

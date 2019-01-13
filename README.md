# Javascript - ES5 and beyond

Javascript ES5(ECMAscript 5) was released in December 2009, which was 10 years after the previous version, ES3.

## ES6/ES2015

This version was released in June 2015, hence the name ES2015. It was decided that the names for the different version will now coincide with the year of release to make it easier to understand... maybe.

## ES2015

So now I will go through examples of the new features and where I have used them in my code.

### let and const

The `const` keyword will not be hoisted and cannot reassigned or redeclared.

```js
export const TOGGLE_FAVOURITE = "TOGGLE_FAVOURITE";
export const ADD_FAVOURITE = "ADD_FAVOURITE";
export const DELETE_FAVOURITE = "DELETE_FAVOURITE";
```

Example of the usage of the `const` keyword in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/actions/beer-actions.js)

The `let` keyword will not be hoisted, cannot be redeclared but can be reassigned.

```js
if (type.includes("FETCH")) {
        let url;
        if (type.includes(BEERS_BY_NAME)) {
            url = `${byNameUrl}${payload.replace(" ", "_")}`;
        }
        if (type.includes(BEER_RANDOM)) {
            url = `${byIdsUrl}${getRandomIds(payload)}`;
        }
```

Example of the usage of the `let` keyword in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/middleware/beer-middleware.js)

### Arrow Functions

```js
export const fetchBeerRandom = numberOfBeers => ({
    type: FETCH_BEER_RANDOM,
    payload: numberOfBeers,
    meta: {
        feature: BEER_RANDOM
    }
});

export const setBeers = (beers, feature) => ({
    type: `${feature}${SET_BEERS}`,
    payload: beers,
    meta: {
        feature,
        normalizeKey: "id"
    }
});
```

Example of the usage of arrow functions in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/actions/beer-actions.js)

### Template Literals

```js
const getRandomIds = noOfIds =>
    new Array(Number(noOfIds))
        .fill(0)
        .map(n => n + Math.floor(Math.random() * 234 + 1))
        .reduce((acc, number) => {
            acc = `${acc}${number}${"|"}`;
            return acc;
        }, "");
```

Example of the usage of arrow functions in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/middleware/beer-middleware.js)

### Implicit Function Returns

```js
export const getNeededBeerProperties = beerList =>
    beerList.map(({ image_url, name, id, tagline }) => ({
        image_url,
        name,
        id,
        tagline
    }));

export const getNoOfFavourites = state =>
    Object.keys(state.beers.favouriteBeers).length;
```

Example of the usage of implicit returns in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/selectors/selectors.js)

### Key/Property Shorthand

```js
export const apiRequest = (body, method, url, feature) => ({
    type: `${feature}${API_REQUEST}`,
    payload: body,
    meta: {
        method,
        url,
        feature
    }
});
```

Example of the usage of property shorthand in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/actions/api-actions.js)

### Method Definition Shorthand

```js
const mapDispatchToProps = dispatch => ({
    getRandomBeers(noOfBeers) {
        dispatch(fetchBeerRandom(noOfBeers));
    },
    updateNoOfRandomBeers(noOfBeers) {
        dispatch(updateNoOfRandomBeers(noOfBeers));
    }
});
```

Example of the usage of method definition shorthand in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/components/random-bar.js)

### Destructuring

```js
function BeerCard({ classes, beer, isFavourite, toggleFavourite }) {
    const { card, content, star, icon, action } = classes;
    const { image_url, name, id, tagline } = beer;
    return (
        <Card className={card}>
            <Image src={image_url}
                alt={name}
                style={clearImagePadding}
                imageStyle={imageStyle} />
// etc
```

Example of the usage of destructuring in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/components/beer-card.js)

### Default Parameters

```js
export const isLoading = (state = false, action) =>
    action.type.includes(SET_LOADER) ? action.payload : state;

export const noOfRandomBeers = (state = "5", action) => {
    switch (true) {
        case action.type.includes(UPDATE_NO_OF_RANDOM_BEERS):
            return action.payload;
        default:
            return state;
    }
};
```

Example of the usage of default parameters in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/reducers/ui-reducer.js)

### Spread Syntax

```js
const getBeers = field => state => {
    const requiredBeers = state.beers[field];
    return (
        Object.keys(requiredBeers).reduce((beers = [], beerId) => {
            const { id, name, tagline, image_url } = requiredBeers[beerId];
            return [
                ...beers,
                {
                    id,
                    name,
                    tagline,
                    image_url
                }
            ];
        }, []) || []
    );
};
```

Example of the usage of array spread in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/selectors/selectors.js)

```js
export const favouriteBeers = (state = {}, action) => {
    switch (action.type) {
        case ADD_FAVOURITE:
            return {
                ...state,
                ...action.payload
            };
        case DELETE_FAVOURITE:
            const { [action.payload]: value, ...rest } = state;
            return rest;
        case `${"INIT"}${LOAD_FROM_LOCAL_STORAGE_SUCCESS}`:
            return action.payload;

        default:
            return state;
    }
};
```

Example of the usage of object spread in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/middleware/normalize-middleware.js)

### Modules import/export

```js
import React from "react";

const Loading = () => {
    return (
        <div style={{ display: "grid" }}>
            <i
                className="fa fa-spinner fa-3x fa-spin"
                style={{
                    marginLeft: "auto",
                    marginRight: "auto",
                    marginTop: 20
                }}
            />
        </div>
    );
};

export default Loading;
```

Example of the usage of object spread in my project [here](https://github.com/martinbryant/beer_engineer/blob/master/src/components/loading.js)

### Array Iteration

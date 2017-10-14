# Point of Sale in Java at \#jbhc17

This contains a sample "solution" for the Point of Sale exercise in Java
as performed at [#jbhc17](https://twitter.com/search?q=%23jbhc17).

## Features

Look in `documents/Point of Sale Features.markdown` for an inbox of
features. This project started with "Sell One Item".

## Architecture

The project consists of a `HappyZone` module where nothing
depends on anything outside the _happy zone_. Everything that integrates
with the _horrible outside world_ resides in `DemilitarizedZone`.

## Testing

The project uses Spock Framework primarily for data-driven testing
and JUnit otherwise. The maintainers acknowledge this as a purely
arbitrary decision based on inertia. (I know and like JUnit; I don't
consider myself a `groovy` expert; I'd rather learn Kotlin, anyway,
but today is not the day for that.)


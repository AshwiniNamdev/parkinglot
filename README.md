

## About Problem

To **design a parking lot system** with ability to find:

- Registration numbers of all cars of a particular colour.

- Slot number in which a car with a given registration number is parked.

- Slot numbers of all slots where a car of a particular colour is parked.

[![Parking Lot]](https://github.com/ashwininnamdev/ParkingLot/)

## Pre requisites

The source code for this project is written using [Node.js](https://nodejs.org/). Make sure you have [Node.js](https://nodejs.org/) installed on your computer before running this application, **if not please install Node.js from [here](https://nodejs.org/en/download/)**.

To check if you have Node.js and NPM installed by running simple commands to see what version of each is installed:

 - **Test Node.js**: To see if Node is installed, type `node -v` in Terminal. This should print the version number so you’ll see something like this `v14.16.0`.

 - **Test NPM**. To see if NPM is installed, type `npm -v` in Terminal. This should print the version number so you’ll see something like this `6.9.0`.

> **Note:** [Node installer](https://nodejs.org/en/download/) installs both Node.js and npm on your system.

## How to run?

This is a console application written in `Node.js`. This can be run in two modes:

1. **Interactive Mode**: An interactive terminal based shell where commands can be typed in to perform different actions.

2. **File Mode**: It accepts a filename as a parameter at the terminal and read the commands from that file.

### Quick Start

**Proceed to the steps below only if you've `Node.js` installed.** If not, please refer [pre requisites](#pre-requisites) section.

#### For Interactive Mode

Open terminal and navigate (`cd`) to this folder and type the following commands:

```bash
1. npm install
2. npm start
```

#### For File Mode

Open terminal and type `node src/index.js data/input.txt`.

```terminal
node src/index.js <path_to_file.txt>
```

**Note**: You can find a few sample input files inside `data/` folder.

#### Explained

**STEP 1**: `npm install` or `npm i` will download all the dependencies defined in `package.json` file and generate a `node_modules/` folder with the installed modules. Learn more [here](https://docs.npmjs.com/cli/install).

**STEP 2**: `npm start` or `npm run start` will start the application. It is equivalent to `node src/index.js`

## List of User Commands

Users can interact with the Parking Lot system via a following simple set of commands which produce a specific output:

- **create_parking_lot**: `create_parking_lot 6` will create a parking lot with 6 slots.

- **park < REGISTRATION NUMBER > < COLOR >**: `park KA-01-HH-1234 White` will allocate the nearest slot from entry gate.

- **leave**: `leave 4` will make slot number 4 free.

- **status**: `status` will display cars and their slot details

```bash
Slot No.  Registration No Color
1         KA-01-HH-1234  White
2         KA-01-HH-9999  Red
3         KA-01-BB-0001  White
5         KA-01-HH-2701  Black
6         KA-01-HH-3141  Black
```

- **registration_numbers_for_cars_with_colour < COLOR >**: `registration_numbers_for_cars_with_colour White` will display the registration number of the cars of white color e.g. `KA-01-HH-1234, KA-01-BB-0001`

- **slot_numbers_for_cars_with_colour < COLOR >**: `slot_numbers_for_cars_with_colour White` will display slot numbers of the cars of white color e.g. `1, 3`

- **slot_number_for_registration_number < REGISTRATION NUMBER >**: `slot_number_for_registration_number MH-04-AY-1111` will display the slot number for the car with registration number MH-04-AY-1111.

- **leave_car_by_registration_number**: `leave_car_by_registration_number JH-01-LT-0008` will free the slot occupied by car with registration number JH-01-LT-0008.

- **available_slot_numbers**: `available_slot_numbers` will display available slot numbers e.g. 2, 6, 8.

- **allocated_slot_numbers**: `allocated_slot_numbers` will display occupied slot numbers e.g. 1, 3, 4, 5, 7.

- **exit**: `exit` will quit the application and return to the console.

> **NOTE: Any commands which are not mentioned above will throw an error: `<INPUT> is an invalid command`**

**To view all the commands in terminal, please run `npm run help`**

## Modules - OOPS Approach

There are two classes defined:

`ParkingLot()`: It is the main class which is used to initialize a parking lot. In each parking lot there is maximum number of slots and an array of slots that will be occupied by the car. It has following methods:

- `createParkingLot(input)` : Creates a parking lot with given input. It throws an error `Minimum one slot is required to create parking slot` if zero or negative number (n <= 0) is provided as an input.

- `parkCar(input)` : Allocates nearest slot from entry gate to the car. It can throw following errors:

    - `Minimum one slot is required to create parking slot` : When parking lot is not initialized.

    - `Sorry, parking lot is full` : When parking lot has reached its maximum capacity.

    - `Please provide registration number and color both` : When input contains either of two i.e. registration number and color of the car, not both.

- `leaveCar(input)` : Removes car in given slot in parking lot. It throws following errors:

  - `Sorry, parking lot is empty` if parking lot is empty.

  - `Slot number <SLOT NUMBER> is not found` when slot number is absent.

  - `Slot number <SLOT NUMBER> is already free` when slot number is not occupied.

- `leaveCarByCarNumber (input)` : Makes the slot free for car of given registration number.

- `getParkingStatus()` : Returns an array containing slot number, registration number and color. It throws an error `Sorry, parking lot is empty` if parking lot is empty.

- `getCarsWithSameColor(input)` : Returns a comma separated string containing registration numbers of cars with same color e.g. `KA-01-HH-1234, KA-01-HH-9999, KA-01-P-333`.

- `getSlotsWithSameColorCar(input)` : Returns a comma separated string containing slot numbers of car with same color e.g. `3, 5, 6`.

- `getSlotByCarNumber(input)` : Finds slot number of car for given registration number. It returns `Not found` when car is not present.

- `findNearestAvailableSlot()` : Finds nearest free slot.

- `findAllAvailableSlots()` : returns a comma separated string of free parking slots e.g. 1, 4, 7. It returns `null` if parking lot is not created.

- `findAllAllocatedSlots()` : returns a comma separated string of allocated parking slots e.g. 2, 3, 5, 6. It returns `null` if parking lot is not created.

`Car()`

- `new Car(NUMBER, COLOR)` : Constructor used to initialize a car object containing two fields, registration number and color.

- `isCarEqual()` : Checks whether two cars are equal or not.

**Note:** *I've made an assumption that the registration number for two cars can never be same.*

## Test Scripts

Tests are written using [Mocha](https://mochajs.org/) and can be run using `npm test`

- `npm run test-unit` : Run unit tests only (Tests for functions in Parking Class)
- `npm run test-system` : Run repository tests only (See [this](#system-tests) section)
- `npm run test-lint` : Run lint tests using ESLint
- `npm run test` : Run all tests (lint tests + unit tests + system tests)

#### Unit tests

Unit tests are written for the methods of `ParkingLot` class.

#### System tests

System tests mainly include repository structure tests. It tests for the following:

Repository must contain:

- `package.json`
- `README.md`
- `.gitignore`
- `.eslintrc`
- `npm/` folder
- `src/` folder
- `tests/` folder

`package.json`

`.gitignore` must contain `build/`, `dist/`, `out/`, `node_modules/` folders.

#### Lint tests

`npm run test-lint` is used to run JavaScript lint tests. It detects the coding style issues. ESLint rules are defined in `.eslintrc.js` file.

`node_modules/eslint/bin/eslint.js --fix src/` can be run to fix lint errors.

## TL; DR

Open terminal and type the following:

1. `cd parking_lot` : Navigates to the `parking_lot` root folder.

2. `npm install` : Installs all the dependencies.

3. `npm run start` : Starts the console application in interactive mode.

4. `npm run test` : Runs all the tests.

5. `npm run test-unit` : Runs all the unit tests.

6. `npm run test-system` : Runs system tests.

7. `npm run test-lint` : Runs lint test.

8. `npm run build` : Builds the application in `bin/` directory.

9. `npm run create-docs` : Creates documentation inside `out/` folder.

10. `npm run help` : Displays all supported user commands.

11. `node src/index.js data/input.txt` : Runs the application in file mode.
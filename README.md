# Philosophers 🍽️

Philo is a threading project that simulates the famous "Dining Philosophers" problem. It demonstrates fundamental concepts in concurrent programming, mutex synchronization, thread management, and deadlock prevention. The goal is to prevent philosophers from starving while respecting the constraint that each fork can only be used by one philosopher at a time.

## Table of contents

- [Highlights](#highlights)
- [Functions](#functions)
- [Definitions](#definitions)
- [Installation](#installation)
- [Usage](#usage)
- [Testing](#testing)

## Highlights

- Simulate multiple philosophers eating and thinking concurrently
- Implement mutex-based synchronization to prevent race conditions
- Prevent deadlocks and starvation scenarios
- Monitor philosopher states in real-time
- Support configurable timing parameters (time to die, eat, sleep)
- Precise timestamp logging for all actions
- Thread-safe data structures with proper locking mechanisms
- Handle edge cases: odd/even philosopher counts, extreme timing values

## Definitions

| Term | Description |
|------|-------------|
| Philosopher | A thread that alternates between eating and thinking |
| Fork | A shared resource (mutex) that two adjacent philosophers compete for |
| Mutex | A synchronization primitive that ensures only one thread accesses a resource |
| Thread | A lightweight process running concurrently |
| Race Condition | Unexpected behavior when multiple threads access shared data simultaneously |
| Deadlock | A situation where threads wait indefinitely for resources held by other threads |
| Starvation | A philosopher never gets to eat and eventually dies |
| Timestamp | The exact time an action occurred (in milliseconds) |
| State | The current condition of a philosopher (eating, thinking, sleeping, dead) |
| Simulation | The entire process of all philosophers interacting over time |

## Functions

### Core Functions

**main**: Validates arguments and starts the simulation

**init_simulation**: Initializes the simulation structure and philosopher threads

**init_forks**: Creates mutex objects for each fork

**philo_routine**: Main thread function executed by each philosopher

**philo_actions**: Handles philosopher actions (eating, thinking, sleeping)

**philo_monitoring**: Monitors all philosophers and detects deaths/completion

**ft_atol**: Converts string to long integer with overflow protection

**is_digit**: Validates that a string contains only digits

**get_timestamp**: Retrieves current time in milliseconds

**print_status**: Safely prints philosopher actions with proper formatting

**destroy_mutex**: Cleans up and unlocks all mutex objects

**free_resources**: Deallocates memory and terminates threads

## Installation

Clone the repository:
```bash
git clone git@github.com:ver0niqueg/42-Philosophers.git
cd 42-Philosophers
```

Compile:
```bash
make
```

Clean object files:
```bash
make clean
```

Remove all generated files:
```bash
make fclean
```

Recompile:
```bash
make re
```

## Usage

Run with required arguments:
```bash
./philo <number_of_philosophers> <time_to_die> <time_to_eat> <time_to_sleep> [number_of_times_each_philosopher_must_eat]
```

### Parameters

- `number_of_philosophers`: Number of philosophers (1-200)
- `time_to_die`: Time in milliseconds before a philosopher dies if they haven't eaten
- `time_to_eat`: Time in milliseconds it takes to eat
- `time_to_sleep`: Time in milliseconds a philosopher sleeps
- `number_of_times_each_philosopher_must_eat`: (Optional) Stops simulation when all philosophers have eaten this many times

### Examples

```bash
# Simple test with 4 philosophers
./philo 4 400 200 200

# With eating limit (program stops after each philosopher eats 5 times)
./philo 5 800 200 200 5

# Challenging scenario (tight timings)
./philo 4 200 100 100

# Easy scenario (relaxed timings)
./philo 2 1000 200 200 5

# Odd number of philosophers
./philo 3 600 150 150

# Large number of philosophers
./philo 50 1000 200 200 1
```

## Testing

### What to look for

✅ **No resource conflicts**: Forks aren't used by two philosophers simultaneously  
✅ **Proper synchronization**: All actions are logged with correct timestamps  
✅ **No deadlocks**: Program doesn't hang indefinitely  
✅ **No starvation**: All philosophers get a chance to eat  
✅ **Clean termination**: Program exits gracefully when conditions are met  
✅ **Death detection**: Program stops immediately when a philosopher dies  

### Test scenarios

**Basic functionality**:
```bash
./philo 4 800 200 200 10
```
Expected: 4 philosophers eat 10 times each, program terminates.

**Death scenario**:
```bash
./philo 4 400 200 200
```
Expected: A philosopher dies and program stops with death message.

**Starvation test**:
```bash
./philo 5 100 50 50
```
Expected: Program handles extreme timing without deadlock.

**Single philosopher**:
```bash
./philo 1 400 200 200
```
Expected: Philosopher sits, thinks, takes fork, dies (can't eat with only 1 fork).

**Two philosophers**:
```bash
./philo 2 1000 200 200
```
Expected: Both philosophers can eat alternately.

## Philosopher Status Messages

The program outputs messages in the following format:
```
[timestamp_in_ms] [philosopher_id] [action]
```

| Action | Description |
|--------|-------------|
| `is thinking` | Philosopher is in thinking state |
| `has taken a fork` | Philosopher picked up a fork |
| `is eating` | Philosopher is eating |
| `is sleeping` | Philosopher is sleeping |
| `died` | Philosopher has starved to death |

### Example output
```
0 1 is thinking
0 2 is thinking
0 3 is thinking
0 4 is thinking
0 5 is thinking
100 1 has taken a fork
100 1 has taken a fork
100 1 is eating
200 2 has taken a fork
200 2 has taken a fork
200 2 is eating
```

## Key Concepts

### Mutex Synchronization
- Each fork is protected by a mutex to ensure only one philosopher can use it at a time
- Print operations use a dedicated mutex to prevent garbled output
- Philosopher state updates use mutexes for thread-safe access

### Deadlock Prevention
- Philosophers acquire forks in a consistent order
- Proper timeout and monitoring to detect issues early
- Release locks immediately after use

### State Management
- Each philosopher tracks: ID, meals eaten, last meal time, state
- Central death flag monitored by all threads
- Meal counter to track completion condition

---

vgalmich – 42 School Student

# Simple Timer in C++

This C++ program creates a basic timer that displays hours, minutes, and seconds, counting up from 00:00:00. The timer updates every second and shows the elapsed time in a formatted view.

## Features

- **Time Display**: The timer displays hours, minutes, and seconds in the format `hh : mm : ss`.
- **Real-Time Update**: The display refreshes each second to show the updated time.
- **Infinite Counting**: The timer counts indefinitely until manually terminated.

## How It Works

- The program uses a `while` loop to increment seconds, minutes, and hours.
- The `displayClock()` function is called each second to clear the screen and print the updated time in a formatted structure.
- A system call, `system("cls")`, clears the screen on Windows. For other operating systems, replace `"cls"` with `"clear"`.

## Code

```cpp
#include <iomanip>
#include <iostream>
#include <thread>         // std::this_thread::sleep_for

using namespace std;

// hours, minutes, seconds of timer
int hours = 0;
int minutes = 0;
int seconds = 0;

// function to display the timer
void displayClock()
{
    system("cls");
    cout << setfill(' ') << setw(55) << "         TIMER         \n";
    cout << setfill(' ') << setw(55) << " --------------------------\n";
    cout << setfill(' ') << setw(29);
    cout << "| " << setfill('0') << setw(2) << hours << " hrs | ";
    cout << setfill('0') << setw(2) << minutes << " min | ";
    cout << setfill('0') << setw(2) << seconds << " sec |" << endl;
    cout << setfill(' ') << setw(55) << " --------------------------\n";
}

void timer()
{
    while (true) {
        displayClock();
        this_thread::sleep_for(chrono::seconds(1));

        seconds++;
        if (seconds == 60) {
            minutes++;
            seconds = 0;
            if (minutes == 60) {
                hours++;
                minutes = 0;
            }
        }
    }
}

int main()
{
    timer();
    return 0;
}
```

## Usage

1. **Compile the Program**:
   ```bash
   g++ -o timer timer.cpp
   ```

2. **Run the Timer**:
   ```bash
   ./timer
   ```

3. **Stop the Timer**:
   - Press `Ctrl + C` to stop the timer on Linux or Windows.

## Requirements

- **C++11 or later**: This program requires C++11 for `chrono` and `thread` libraries.

## Notes

- **Screen Clearing**: This program uses `system("cls")` to clear the screen on Windows. If you’re on a Unix-based system (e.g., Linux, macOS), replace `system("cls")` with `system("clear")` in the `displayClock()` function.
- **Indefinite Run**: This timer runs indefinitely, displaying real-time updates every second. To stop, press `Ctrl + C`.

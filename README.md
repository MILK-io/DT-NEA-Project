# DT-NEA-Project

# Arduino Multi-LCD Quiz Game

## Overview
This Arduino-based interactive quiz game uses multiple I2C LCD displays to create an engaging educational experience for children. The game features:

- 5 LCD displays (20x4 character size) - one for questions and four for answer choices
- 5 buttons for interaction - one control button and four answer buttons
- Three subject categories: Maths, Science, and Geography
- Three difficulty levels: Ages 4-6, Ages 7-9, and Ages 10-12
- Score tracking system with points for correct/incorrect answers
- Simple interface with visual feedback

## Hardware Requirements
- Arduino board (Uno, Mega, or similar)
- 5 LCD displays (20x4) with I2C adapters
 - Question display (I2C address: 0x27)
 - Answer A display (I2C address: 0x26)
 - Answer B display (I2C address: 0x25)
 - Answer C display (I2C address: 0x24)
 - Answer D display (I2C address: 0x23)
- 5 push buttons
- Jumper wires
- Breadboard or custom PCB
- 5V power supply (capable of powering all LCDs)

## Wiring Instructions
1. **I2C Connection**
  - Connect SDA pins of all LCDs to the Arduino's SDA pin
  - Connect SCL pins of all LCDs to the Arduino's SCL pin
  - Connect VCC pins of all LCDs to 5V
  - Connect GND pins of all LCDs to ground

2. **Button Connections**
  - Control button: Connect between digital pin 2 and ground
  - Answer A button: Connect between digital pin 3 and ground
  - Answer B button: Connect between digital pin 4 and ground
  - Answer C button: Connect between digital pin 5 and ground
  - Answer D button: Connect between digital pin 6 and ground

**Note:** All buttons use the Arduino's internal pull-up resistors, so no external resistors are needed.

## Software Setup
1. Install the required libraries:
  - Wire.h (included with Arduino IDE)
  - LiquidCrystal_I2C.h (can be installed via Library Manager)

2. Download and open the quiz game code in the Arduino IDE

3. Verify and upload the code to your Arduino board

## Customizing the Quiz
The quiz questions are organized into arrays by subject and difficulty level:
- `mathQuestions_easy`, `mathQuestions_medium`, `mathQuestions_hard`
- `scienceQuestions_easy`, `scienceQuestions_medium`, `scienceQuestions_hard`
- `geoQuestions_easy`, `geoQuestions_medium`, `geoQuestions_hard`

To add or modify questions:
1. Locate the appropriate array based on the subject and difficulty level
2. Each question is defined with:
  - Question text (can include `\n` for line breaks)
  - Four answer choices in an array
  - The index of the correct answer (0-3, where 0 is the first answer)

Example:
```cpp
{"What is 5 + 7?", {"10", "11", "12", "13"}, 2}  // Answer: 12 (index 2)
```

## Using the Game
1. **Starting the Game**
  - When powered on, the game displays welcome instructions
  - After 3 seconds, it shows the status screen with current topic, level, and score
  - After 5 seconds, the first question appears

2. **Game Controls**
  - **Answer Buttons (A, B, C, D)**: Press to select an answer
  - **Control Button (Single Click)**: Reset score to zero
  - **Control Button (Double Click)**: Change question category (Maths → Science → Geography)
  - **Control + Any Answer Button**: Change difficulty level (Ages 4-6 → Ages 7-9 → Ages 10-12)

3. **Scoring System**
  - Correct answer: +10 points
  - Incorrect answer: -5 points (minimum score is 0)

4. **Display Feedback**
  - Correct answers: The selected answer display flashes three times
  - Incorrect answers: The selected answer display flashes three times
  - Text feedback appears on the question display

## I2C Address Troubleshooting
If your LCDs have different I2C addresses than specified in the code:

1. Run an I2C scanner sketch (available in many I2C library examples) to identify the actual addresses of your LCDs

2. Update the addresses in the code:
```cpp
LiquidCrystal_I2C questionLCD(0x27, 20, 4);  // Change 0x27 to your address
// Update other LCD addresses as needed
```

## Extending the Game
- **More Questions**: Add more questions to each array or create new question categories
- **Timer Feature**: Implement a time limit for answering questions
- **Sound Effects**: Add a buzzer for audio feedback
- **High Score Tracking**: Use EEPROM to save and display high scores
- **Multiple Choice Types**: Add true/false or numeric entry questions

## Notes on Question Display
- Questions can be up to  40 characters (2 lines of 20 characters each)
- Use `\n` in the question text to force a line break
- Answers display on separate LCDs, allowing for longer answer texts


## Technical Details
- Button debouncing is implemented to prevent multiple triggers
- Double-click detection uses time-based logic
- Display flashing provides visual feedback for answers
- Question cycling loops back to the beginning after reaching the end

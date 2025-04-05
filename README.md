# Ducky-8-Ball
 Magic 8-Ball application on the DuckyPad Pro

// --- Magic 8-Ball Script for duckyPad ---

// Declare global variables
VAR $answer = 0      // Stores the random number for the answer choice
VAR $key_pressed = 0 // Stores the ID of the key pressed by the user

// Main script loop - runs indefinitely
WHILE 1

  // --- Display Initial Prompt ---
  OLED_CLEAR             // Clear the OLED display buffer
  OLED_CURSOR 0 0        // Set cursor to top-left (x=0, y=0)
  OLED_PRINT "Magic 8-Ball!" // Print the title
  OLED_CURSOR 0 16       // Move cursor down (y=16)
  OLED_PRINT "Press any key..." // Print the prompt
  OLED_UPDATE            // Update the physical OLED screen

  // --- Wait for User Input ---
  // Wait indefinitely until any key is pressed and store its ID
  $key_pressed = $_BLOCKING_READKEY

  // --- Check for Halt Condition ---
  // Check if the pressed key is the upper rotary encoder button (ID 23)
  IF $key_pressed == 23 THEN
    OLED_CLEAR           // Clear the screen
    OLED_CURSOR 0 16     // Position cursor
    OLED_PRINT "Script Halted." // Display halt message
    OLED_UPDATE          // Update the screen
    DELAY 1000           // Pause for 1 second to show the message
    HALT                 // Stop script execution completely
  END_IF // End of halt check

  // --- Process Input (if not halted) ---
  OLED_CLEAR             // Clear screen for the next message
  OLED_CURSOR 0 16       // Position cursor
  OLED_PRINT "Thinking..."    // Display "Thinking..." message
  OLED_UPDATE            // Update the screen
  DELAY 500              // Pause for 0.5 seconds

  // --- Generate Random Answer ---
  $_RANDOM_MIN = 1       // Set minimum random number (inclusive)
  $_RANDOM_MAX = 8       // Set maximum random number (inclusive)
  $answer = $_RANDOM_INT // Get the random integer and store it

  // --- Display Answer ---
  OLED_CLEAR             // Clear screen for the answer
  OLED_CURSOR 0 16       // Position cursor

  // Select and print the answer based on the random number
  IF $answer == 1 THEN
    OLED_PRINT "It is certain."
  ELSE IF $answer == 2 THEN
    OLED_PRINT "Reply hazy, try again."
  ELSE IF $answer == 3 THEN
    OLED_PRINT "Don't count on it."
  ELSE IF $answer == 4 THEN
    OLED_PRINT "Signs point to yes."
  ELSE IF $answer == 5 THEN
    OLED_PRINT "My sources say no."
  ELSE IF $answer == 6 THEN
    OLED_PRINT "Outlook good."
  ELSE IF $answer == 7 THEN
    OLED_PRINT "Ask again later."
  ELSE // Catches $answer == 8
    OLED_PRINT "Very doubtful."
  END_IF // End of answer selection

  OLED_UPDATE            // Update the screen to show the answer

  // --- End of Loop Delay ---
  DELAY 1000             // Pause for 1 second before looping back

END_WHILE // End of main script loop (loops back to display prompt)

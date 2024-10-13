#!/bin/bash

# Load colors and ASCII art
source ./assets/colors.sh
ART=$(<./assets/art.txt)
DATA_FILES=$(<./assets/data_files.txt)
SOUND_ENABLED=false  # Set to true if sound is enabled

# Function to simulate typing effect
typing_effect() {
    local text="$1"
    for (( i=0; i<${#text}; i++ )); do
        printf "${text:i:1}"
        sleep 0.05
    done
    echo
}

# Function to play sound
play_sound() {
    if [ "$SOUND_ENABLED" = true ]; then
        echo -e "\a"  # This generates a beep in most terminal environments
        sleep 0.5
    fi
}

# Function to simulate a progress bar
progress_bar() {
    local duration=$1
    local bar_length=30
    local completed=0

    while [ $completed -le $bar_length ]; do
        sleep $(($duration / $bar_length))
        printf "\r["
        for (( i=0; i<completed; i++ )); do
            printf "="
        done
        for (( i=completed; i<bar_length; i++ )); do
            printf " "
        done
        printf "] %d%%" $(( 100 * completed / bar_length ))
        ((completed++))
    done
    echo -e "\n"
}

# Start the hacking simulation
clear
echo -e "${PURPLE}$ART${RESET}"
echo -e "${CYAN}Initializing hacking simulation...${RESET}"
sleep 1

# Mission Briefing
echo -e "${YELLOW}Mission Briefing:${RESET}"
typing_effect "Your objective is to infiltrate the target database and retrieve valuable user data."
sleep 2

# Connection Phase
echo -e "${GREEN}Attempting to connect to the database...${RESET}"
for i in {1..5}; do
    sleep 1
    echo -e "${BLUE}[INFO] Attempting connection... (${i}/5)"
    if (( RANDOM % 2 )); then  # Randomly succeed or fail
        echo -e "${GREEN}[SUCCESS] Connected to the target database!${RESET}"
        break
    else
        echo -e "${RED}[ERROR] Connection attempt ${i} failed! Retrying...${RESET}"
    fi
done

# Check if connection was successful
if (( i == 5 )); then
    echo -e "${RED}[FATAL] Unable to connect to the database. Exiting simulation...${RESET}"
    exit 1
fi

# Data Download Simulation
echo -e "${YELLOW}Retrieving data files...${RESET}"
IFS=$'\n' read -d '' -r -a files <<< "$DATA_FILES"  # Read data files into an array

while true; do
    echo -e "${CYAN}Available files for download:${RESET}"
    for index in "${!files[@]}"; do
        echo -e "${GREEN}${index}. ${files[index]}${RESET}"
    done
    echo -e "${YELLOW}Enter the number of the file you wish to download (or type 'exit' to quit):${RESET}"
    read -r user_input

    if [[ "$user_input" == "exit" ]]; then
        echo -e "${CYAN}Ending session...${RESET}"
        break
    elif [[ "$user_input" =~ ^[0-9]+$ ]] && (( user_input >= 0 && user_input < ${#files[@]} )); then
        file="${files[user_input]}"
        echo -e "${BLUE}Downloading ${file}...${RESET}"
        
        # Simulate download success or failure
        if (( RANDOM % 4 )); then  # 75% chance of success
            progress_bar 3
            echo -e "${GREEN}[SUCCESS] ${file} downloaded successfully!${RESET}"
            play_sound
        else
            echo -e "${RED}[ERROR] Failed to download ${file}. Retry later!${RESET}"
        fi
    else
        echo -e "${RED}Invalid input. Please enter a valid number.${RESET}"
    fi
done

# Conclusion
echo -e "${CYAN}Data retrieval process complete!${RESET}"
echo -e "${YELLOW}Thank you for participating in the simulation!${RESET}"

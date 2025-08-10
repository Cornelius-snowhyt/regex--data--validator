# regex--data--validator
A Python script that validates names, emalis, phone numbers, dates and addresses using regex in single program.
**Features**
Name validation: Support hyphenated names (Appia-Kubi) and apostrophes (O'Connor)
Email: Checks proper email structure(appiakubi4u@yahoo.com)
Phone number validation: supports international formats(+233 20 199 3236) and allows hyphens, spaces and area codes in brackets((020) 199-3236)
Date & Time validation: Work with 24- hour format(2025-08-11 23;59), also works with 12- hour AM/PM format(2025/08/11 11:59 PM) and accepts -/ or\ as date separators.
Digital Address validation: Stricts checks- invalid dates like 2025-02-30 or invalid times like 25:00 are rejected.


import re
from datetime import datetime

print("  CORNELIUS-SNOWHYT'S All in one Data Validator")
print("= * 50")

# -----Regex Patterns-------
patterns = { 
    "Name": r"^[A-Za-z]+(?:[-' ][A-Za-z]+)*$",

    "Email": r"^[\w\.-]+@[\w\.-]+\.\w{2,}$",

    "Phone Numbers": r"^\+?\d{1,4}?[ -]?\(?\d{1,5}\)?[ -]?\d{1,5}[ -]?\d{1,9}$",


    "Date & Time": r"^\d{4}[-/\\]\d{2}[-/\\]\d{2} (([01]\d|2[0-3]):[0-5]\d|0?[1-9]:[0-5]\d ?[APap][Mm])$",
    
    "Didital Address": r"^[A-Za-z0-9\s,.-]{5,100}$"

}

#----Validation function-----
def validate(field, pattern, value):
    if re.fullmatch(pattern, value):
        if "Date & Time" in field:
            formats = [
                "%Y-%m-%d %H:%M",
                "%Y/%m/%d %H:%M",
                "%Y\\%m\\%d %H:%M",
                "$Y-%m-%d %I:%M %p",
                "%Y/%m/%d $I:$M %p",
                "%Y//%m//%d %I:%M %p"
            ]
            for fmt in formats:
                try:
                   datetime.strptime(value, fmt)
                   return True
                except ValueError:
                   continue
            return False
        return True
    return False

#----Main Loop------
for field, pattern in patterns.items():
    value = input(f"Enter {field}: ").strip()
    if validate(field, pattern, value):
        print(f"{field} is valid.")
    else:
        print(f"{field} is invalid")
print("\nValidation complete. Thank you for using CORNELIUS-SNOWHYT's Validator!")  


Valid Input Example
==================================================
  CORNELIUS-SNOWHYT'S All in one Data Validator
= * 50
Enter Name: Appia-Kubi
Name is valid.
Enter Email: appiakubi4u@yahoo.com
Email is valid.
Enter Phone Numbers: +233201993236
Phone Numbers is valid.
Enter Date & Time: 2025-08-11 22:58    
Date & Time is valid.
Enter Didital Address: EZ-0376-1335
Didital Address is valid.

Validation complete. Thank you for using CORNELIUS-SNOWHYT's Validator!
snow@snow-Lenovo-IdeaPad-U410-Touch:~/Documents$ 

Invalid Input Example
  CORNELIUS-SNOWHYT'S All in one Data Validator
= * 50
Enter Name: Appia@Kubi
Name is invalid
Enter Email: test#.com
Email is invalid
Enter Phone Numbers: +233230987
Phone Numbers is valid.
Enter Date & Time: 2025-13-14 25:29
Date & Time is invalid
Enter Didital Address: EZ$$$$$  
Didital Address is invalid

Validation complete. Thank you for using CORNELIUS-SNOWHYT's Validator!
snow@snow-Lenovo-IdeaPad-U410-Touch:~/Documents$ 


HOW TO RUN
1.Install Python3.
2.Save scripts as validator2.py
3.Run in terminal.

Project Files
**validator2.py-Main validation script
**README.md-
**Documentation

Skills Demonstrated
**Advanced Regex
**Date/Time parsing with Python's datetime
**Input validation for multiple formats
**User friendly CLI interface
**Clean, modular code design

LICENSE
This project is open-source and free to use under the MIT License.

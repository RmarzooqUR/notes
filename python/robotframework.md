# ROBOT FRAMEWORK
A python testing framework that uses natural language to write tests.
Has a library ecosystem ( ex. `SeleniumLibrary` ) and also supports creating custom libraries.

- Libraries have methods that interact with application
    + and can be accessed in tests : methods are mapped to its natural language interpretation.
        + `create_profile` -> `Create Profile`
- `tests` written in `.robot` files.
- `tests` use `keywords` defined by tester or in library
- `keywords` can use `variables` and accept `Arguments`


```robot
*** Settings ***
Test Setup      Clear Database
Library         /path/to/library

*** Test Cases ***
Create Valid Profile        ${VALID USER}       ${VALID PASSWORD}
Login User              ${VALID USER}       ${VALID PASSWORD}

*** Keywords ***
Create Valid Profile
    [Arguments]         ${username}     ${password}
    Create Profile      ${username}     ${password}     //from lib

Login User
    [Arguments]         ${username}     ${password}
    Enter Username      ${username}                     //from lib
    Enter Password      ${password}                     //from lib
    Login


*** Variables ***
${VALID USER}           mojito
${VALID PASSWORD}       P4ssw0rd
```
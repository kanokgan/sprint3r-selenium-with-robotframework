*** Settings ***
Library			Selenium2Library
Suite Setup     Open the login page
Test Setup   	Go to login page
Suite Teardown  Close Browser

*** Variables ***
${LOGIN PAGE}    http://localhost:7272/html/
${ERROR PAGE}    ${LOGIN PAGE}error.html

${ERROR PAGE TITLE}    Error Page
${RIGHT USER}     demo
${RIGHT PASS}     mode
${INVALID INPUT}     abc


*** Testcases ***                   USERNAME            PASSWORD

empty username invalid PWD
    [Tags]     Empty username
	Fill in username and password as    ${EMPTY}    ${INVALID INPUT}
	Click login button
	Error Page should be opened




*** Keywords ***

test case : login fail
	[Arguments]    ${username}    ${password}
	Fill in username and password as    ${username}    ${password}
	Click login button
	Error Page should be opened

Error Page should be opened
	Title Should Be    ${ERROR PAGE TITLE}
	Location Should Be    ${ERROR PAGE}
	Element Should Contain    xpath=//div/h1    ${ERROR PAGE TITLE}


Go to login page
    [Documentation]     xxxxx
    ...                 yyyy
    ...                 zzzz
	Go TO    ${LOGIN PAGE}

Open the login page
	Open Browser   ${LOGIN PAGE}
	Maximize Browser Window
    Set Selenium Speed  0

Fill in username and password as
	[Arguments]    ${username}    ${password}
	Input Text    name=username_field   ${username}
	Input Text    name=password_field   ${password}

Click login button
	Click Button   LOGIN

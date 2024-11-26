![Image](./logo_001.PNG)
# goKraken net document List


#### ARCHITECTURE DIAGRAMS [Architecture Document](./KrakenNet_Architecture_Digrams_(v.0.1).pdf)

  1. High-Level System Architecture Diagram

  1. Detailed Architecture of MOTHER

  1. Data Flow Diagram

  1. Deployment Diagram


#### USER JOURNEYS [User Document](./KrakenNet_User_Journeys_(v.0.1).pdf)

  1. End User Journey - Contributing Idle Computing Power

  1. Developer Journey - Integrating KrakenNet API/SDK

  1. System Interaction Overview

#### RESTFul API Tutorial

###### Objective
  - Describes the usage procedure of the RESTFul API of the Atlas platform that generates media content corresponding to user input using generative AI technology and the detailed API functions.

###### Target
  - Companies / users who want to receive AI-based media content corresponding to input data end-to-end
  - Developers or researchers of services (Web/Mobile/PC) based on HTTP/HTTPS web protocol

##### RESTFul API Tutorial
###### Step-1: Get Token (POST)
1. Description
  - The first step to use the Atlas RESTFul API is to issue an authentication key for the entered account.
  - The issued authentication key must be passed along with the Authorization key in all API headers to enable normal API use.
  - The expiration time (Expiry) of the issued authentication key is 24 hours.
1. Example (Authorization)
  - Request
    curl -X 'POST' \
        'https://api.atg-atlas.com/atlas/auth/sign-in' \
        -H 'accept: application/json' \
        -H 'Content-Type: application/json' \
        -d '{
        "id": "ID",
        "password": "Password"
    }'
- Response
    {
      "accessToken":"Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9"
    }

![Image](./20241001_KrakenNet(v.2.4)_1.png)



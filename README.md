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


### RESTFul API Tutorial
#### Objective
  - Describes the usage procedure of the RESTFul API of the Kraken platform that generates media content corresponding to user input using generative AI technology and the detailed API functions.

#### Target
  - Companies / users who want to receive AI-based media content corresponding to input data end-to-end
  - Developers or researchers of services (Web/Mobile/PC) based on HTTP/HTTPS web protocol


#### Step-1: Get Token (POST)
1. Description
  - The first step to use the Kraken RESTFul API is to issue an authentication key for the entered account.
  - The issued authentication key must be passed along with the Authorization key in all API headers to enable normal API use.
  - The expiration time (Expiry) of the issued authentication key is 24 hours.
1. Example (Authorization)
  - Request
        curl -X 'POST' \
          'https://api.gokraken.net/kraken/auth/sign-in' \
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

#### Step-2: Create AI Model (POST)
  1.  Description
    - Send a request to create AI results based on input data (Video, Image) using the Creation API provided by the Kraken platform.
    - If the creation request is registered normally, the item's unique number (`jobId`) is returned.
    - You can check the item download and creation status using `jobId`.
  1. Example (Video →NeRF2Mesh→ 3DMesh)
    - Request
      curl -X 'POST' \
        'https://api.gokraken.net/kraken/model/nerf2mesh/create' \
        -H 'accept: application/json' \
        -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9' \
        -H 'Content-Type: multipart/form-data' \
        -F 'itemName=NeRFTest' \
        -F 'epoch=50' \
        -F 'payload=@new_dragon.mp4;type=video/mp4'
      
    - Response
        {
            "jobId": "257a59cc-0a3e-4ce7-b7e3-17f3ce6a8041",
            "queueSize": "0",
            "trainingTimePerJob": "10m"
        }
        
#### Step-3 : GET Item Info (GET)
   1. Description
      - Check the item creation status using the item unique number (`jobId`).

   1. Example (Video → NeRF2Mesh → 3DMesh)
      - Request
        curl -X 'GET' \
         'https://api.gokraken.net/kraken/item/my-item/257a59cc-0a3e-4ce7-b7e3-17f3ce6a8041' \
         -H 'accept: application/json' \
         -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9'
        
      - Response
          {
           "jobId": "257a59cc-0a3e-4ce7-b7e3-17f3ce6a8041",
           "itemName": "NeRFTest",
           "model": "nerf2mesh",
           "jobStatus": "success",
           "createdAt": "2024-08-27T14:42:10.845859Z",
           "requestedAt": "2024-08-27T14:38:11.811489Z"
          }


#### Step-4 : Download Item (GET)
  1. Description
      - A creation request is registered and the returned item unique number (`jobId`) is used to download the item.

  1. Example (Video → NeRF2Mesh → 3DMesh)
      - Request
          curl -X 'GET' \
           'https://api.gokraken.net/kraken/item/download/257a59cc-0a3e-4ce7-b7e3-17f3ce6a8041?type=model' \
           -H 'accept: application/octet-stream' \
           -H 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9' \
           --output nerf2mesh.glb
        
    - Response
          HTTP/2 200
          date: Tue, 27 Aug 2024 07:23:55 GMT
          content-type: model/gltf-binary
          content-length: 747160
          content-disposition: attachment; filename=mesh_1.glb
          cache-control: no-cache
    
![Image](./20241001_KrakenNet(v.2.4)_1.png)



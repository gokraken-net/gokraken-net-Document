![Image](./logo_001.PNG)
# goKraken net document List


#### 1. ARCHITECTURE DIAGRAMS [Architecture Document](./KrakenNet_Architecture_Digrams_(v.0.1).pdf)

  1. High-Level System Architecture Diagram

  1. Detailed Architecture of MOTHER

  1. Data Flow Diagram

  1. Deployment Diagram


#### 2. USER JOURNEYS [User Document](./KrakenNet_User_Journeys_(v.0.1).pdf)

  1. End User Journey - Contributing Idle Computing Power

  1. Developer Journey - Integrating KrakenNet API/SDK

  1. System Interaction Overview


#### 3. Detailed Financial Models [Detailed Financial Models](https://github.com/gokraken-net/1.-Detailed-Financial-Models)
    import pandas as pd
    import numpy as np
    
    def calculate_token_emissions(total_supply=1_000_000_000, months=48):
        """Calculate monthly token emissions and financial metrics"""
        
        # Token allocation and prices
        allocations = {
            'seed': {'percentage': 0.05, 'price': 0.04, 'lockup': 6, 'vesting': 18},
            'strategic': {'percentage': 0.10, 'price': 0.06, 'lockup': 3, 'vesting': 15},
            'public': {'percentage': 0.14, 'price': 0.07, 'lockup': 0, 'vesting': 12},
            'ido': {'percentage': 0.06, 'price': 0.08, 'lockup': 0, 'vesting': 3},
            'network_rewards': {'percentage': 0.20, 'vesting': 48},
            'developer_incentives': {'percentage': 0.10, 'vesting': 36},
            'team_advisors': {'percentage': 0.20, 'lockup': 12, 'vesting': 36},
            'operations': {'percentage': 0.10, 'vesting': 48},
            'reserve': {'percentage': 0.05, 'lockup': 24}
        }
        
        # Initialize monthly emission dataframe
        df = pd.DataFrame(index=range(months))
        
        # Calculate emissions for each allocation
        for category, params in allocations.items():
            tokens = total_supply * params['percentage']
            lockup = params.get('lockup', 0)
            vesting = params.get('vesting', 0)
            
            if category == 'ido':
                # Special case for IDO with 50% upfront
                initial_release = tokens * 0.5
                remaining = tokens * 0.5
                monthly = remaining / vesting
                emissions = [0] * lockup + [initial_release] + [monthly] * (vesting - 1)
            else:
                monthly = tokens / vesting if vesting > 0 else 0
                emissions = [0] * lockup + [monthly] * (vesting if vesting > 0 else 1)
            
            df[f'{category}_emissions'] = emissions[:months] + [0] * (months - len(emissions))
        
        # Calculate cumulative metrics
        df['monthly_emissions'] = df.sum(axis=1)
        df['cumulative_supply'] = df['monthly_emissions'].cumsum()
        
        return df

    def project_network_metrics(months=48, initial_users=6000, initial_models=270000):
        """Project network growth and usage metrics"""
        
        # Growth assumptions
        monthly_user_growth = 0.40  # 40% monthly growth
        monthly_model_growth = 0.35  # 35% monthly model growth
        compute_cost_savings = 0.90  # 90% cost savings vs traditional
        
        # Initialize projections dataframe
        df = pd.DataFrame(index=range(months))
        
        # Calculate user and model growth
        df['active_users'] = [initial_users * (1 + monthly_user_growth) ** i for i in range(months)]
        df['models_processed'] = [initial_models * (1 + monthly_model_growth) ** i for i in range(months)]
        
        # Calculate compute metrics
        avg_compute_cost_per_model = 5  # USD
        df['traditional_compute_costs'] = df['models_processed'] * avg_compute_cost_per_model
        df['kraken_compute_costs'] = df['traditional_compute_costs'] * (1 - compute_cost_savings)
        df['cost_savings'] = df['traditional_compute_costs'] - df['kraken_compute_costs']
        
        # Calculate network revenue
        take_rate = 0.20  # 20% platform fee
        df['network_revenue'] = df['kraken_compute_costs'] * take_rate
        
        return df

    def calculate_token_metrics(total_supply=1_000_000_000, initial_price=0.08):
        """Calculate key token metrics"""
        
        emissions_df = calculate_token_emissions(total_supply)
        network_df = project_network_metrics()
        
        # Combine metrics
        df = pd.concat([emissions_df, network_df], axis=1)
        
        # Calculate token metrics
        df['token_price'] = initial_price  # Simplified - would need market dynamics model
        df['market_cap'] = df['cumulative_supply'] * df['token_price']
        df['fully_diluted_valuation'] = total_supply * df['token_price']
        
        return df

    # Generate projections
    projections = calculate_token_metrics()
    
    # Print key metrics for first 12 months
    print("\nMonthly Projections (First Year):")
    print(projections.head(12)[['active_users', 'models_processed', 'network_revenue', 'market_cap']])
    
    # Calculate key statistics
    initial_circulating = projections['cumulative_supply'][0]
    initial_market_cap = initial_circulating * 0.08  # Initial token price
    total_raise = (50_000_000 * 0.04) + (100_000_000 * 0.06) + (140_000_000 * 0.07) + (60_000_000 * 0.08)
    
    print("\nKey Token Metrics:")
    print(f"Initial Circulating Supply: {initial_circulating:,.0f} $INK")
    print(f"Initial Market Cap: ${initial_market_cap:,.2f}")
    print(f"Total Raise: ${total_raise:,.2f}")
    Made with
    Artifacts are user-generated and may contain unverified or potentially unsafe content.
    Report
    Remix Artifact
 
#### 4. Governance Mechanisms [Governance Mechanisms](https://github.com/gokraken-net/2.-Governance-Mechanisms)

##### 1. Governance Structure
###### Voting Power
    - $INK = 1 base vote
    - Voting power multipliers:
      - Staked tokens: 1.5x
      - Network node operators: 2x
      - Active developers: 2x
      - Long-term holders (>6 months): 1.25x

##### Governance Bodies
###### 1. Token Holders
    - All $INK holders
    - Basic voting rights
    - Proposal submission (requires 1M $INK)
###### 2. Technical Committee
    - 7 members
    - Elected by token holders
    - Focus: Technical proposals & upgrades
    - Requirements:
      - Proven technical expertise
      - Min 500K $INK staked
      - 2-year commitment
###### 3. Node Operator Council
    - 5 members
    - Elected by active node operators
    - Focus: Network operations & rewards
    - Requirements:
    - Active node operation
    - Min 3 months history
    - Performance score >95%
###### 4. Development Fund Committee
    - 5 members
    - 3 elected by token holders
    - 2 appointed by core team
    - Focus: Ecosystem fund allocation

##### 2. Proposal System
###### Proposal Types
    1. Network Parameters
    - Reward rates
    - Fee structures
    - Node requirements
    - Threshold: >50% approval
    2. Technical Upgrades
    - Smart contract updates
    - Protocol changes
    - Security implementations
    - Threshold: >66% approval
    3. Treasury Allocation
    - Development grants
    - Marketing initiatives
    - Infrastructure investments
    - Threshold: >60% approval
    4. Emergency Actions
    - Security patches
    - Emergency pauses
    - Threshold: >75% approval
    
###### Proposal Process
    1. Discussion Phase (7 days)
    - Forum discussion
    - Community feedback
    - Technical review
    2. Formal Proposal (3 days)
    - Detailed specification
    - Implementation plan
    - Economic impact analysis
    3. Voting Period (5 days)
    - On-chain voting
    - Real-time results
    - Vote locking
    4. Implementation (if passed)
    - Technical deployment
    - Community notification
    - Progress tracking
##### 3. Economic Rights
###### Fee Distribution
    - 70% to Node Operators
    - 20% to Treasury
    - 10% to Token Burn
###### Staking Benefits
    - Enhanced voting power
    - Fee share participation
    - Priority access to features
###### Developer Incentives
    - Grant access
    - Reduced platform fees
    - Governance participation

##### 4. Risk Management
###### Security Measures
    - Multi-sig requirements
    - Time-locks on major changes
    - Emergency pause mechanisms
###### Checks and Balances
    - Technical Committee veto power
    - Community override mechanism
    - Gradual parameter adjustment

##### 5. Future Governance Evolution
###### Phase 1: Foundation-Guided (Months 1-6)
    - Core team maintains significant influence
    - Focus on stability and growth
    - Community input gathering
###### Phase 2: Community Transition (Months 7-12)
    - Gradual power transfer
    - Committee formations
    - Initial proposal testing
###### Phase 3: Full Decentralization (Month 13+)
    - Complete community governance
    - Core team advisory role
    - Self-sustaining ecosystem

##### 6. Governance Analytics
###### KPIs to Track
    - Proposal participation rate
    - Vote distribution
    - Implementation success rate
    - Community engagement metrics

#### 5. Smart-Contract-Implementation [Smart-Contract-Implementation](https://github.com/gokraken-net/3.-Smart-Contract-Implementation)
          
          // SPDX-License-Identifier: MIT
          pragma solidity ^0.8.17;
          
          import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
          import "@openzeppelin/contracts/access/AccessControl.sol";
          import "@openzeppelin/contracts/security/Pausable.sol";
          import "@openzeppelin/contracts/security/ReentrancyGuard.sol";
          
          /**
           * @title KrakenToken
           * @dev Main token contract for KrakenNet ecosystem
           */
          contract KrakenToken is ERC20, AccessControl, Pausable, ReentrancyGuard {
              bytes32 public constant GOVERNANCE_ROLE = keccak256("GOVERNANCE_ROLE");
              bytes32 public constant OPERATOR_ROLE = keccak256("OPERATOR_ROLE");
              
              uint256 public constant TOTAL_SUPPLY = 1_000_000_000 * 10**18;  // 1B tokens
              
              // Vesting schedule structure
              struct VestingSchedule {
                  uint256 total;
                  uint256 released;
                  uint256 startTime;
                  uint256 cliff;
                  uint256 duration;
                  bool revocable;
              }
              
              // Mapping from address to vesting schedule
              mapping(address => VestingSchedule) public vestingSchedules;
              
              // Staking parameters
              struct Stake {
                  uint256 amount;
                  uint256 startTime;
                  uint256 multiplier;
                  bool isNodeOperator;
              }
              
              mapping(address => Stake) public stakes;
              
              // Events
              event TokensVested(address indexed beneficiary, uint256 amount);
              event TokensStaked(address indexed user, uint256 amount);
              event StakeWithdrawn(address indexed user, uint256 amount);
              event RewardsClaimed(address indexed user, uint256 amount);
              
              constructor() ERC20("KrakenNet", "INK") {
                  _setupRole(DEFAULT_ADMIN_ROLE, msg.sender);
                  _setupRole(GOVERNANCE_ROLE, msg.sender);
                  _mint(msg.sender, TOTAL_SUPPLY);
              }
              
              /**
               * @dev Creates a vesting schedule for an address
               */
              function createVestingSchedule(
                  address beneficiary,
                  uint256 amount,
                  uint256 cliffDuration,
                  uint256 vestingDuration,
                  bool revocable
              ) external onlyRole(GOVERNANCE_ROLE) {
                  require(vestingSchedules[beneficiary].total == 0, "Schedule exists");
                  require(amount > 0, "Amount = 0");
                  
                  vestingSchedules[beneficiary] = VestingSchedule({
                      total: amount,
                      released: 0,
                      startTime: block.timestamp,
                      cliff: cliffDuration,
                      duration: vestingDuration,
                      revocable: revocable
                  });
                  
                  _transfer(msg.sender, address(this), amount);
              }
              
              /**
               * @dev Releases vested tokens for msg.sender
               */
              function releaseVestedTokens() external nonReentrant {
                  VestingSchedule storage schedule = vestingSchedules[msg.sender];
                  require(schedule.total > 0, "No schedule");
                  
                  uint256 releasable = _calculateReleasable(schedule);
                  require(releasable > 0, "Nothing to release");
                  
                  schedule.released += releasable;
                  _transfer(address(this), msg.sender, releasable);
                  
                  emit TokensVested(msg.sender, releasable);
              }
              
              /**
               * @dev Calculates releasable tokens for a schedule
               */
              function _calculateReleasable(VestingSchedule memory schedule) 
                  private 
                  view 
                  returns (uint256) 
              {
                  if (block.timestamp < schedule.startTime + schedule.cliff) {
                      return 0;
                  }
                  
                  if (block.timestamp >= schedule.startTime + schedule.duration) {
                      return schedule.total - schedule.released;
                  }
                  
                  uint256 timeFromStart = block.timestamp - schedule.startTime;
                  uint256 vestedAmount = (schedule.total * timeFromStart) / schedule.duration;
                  
                  return vestedAmount - schedule.released;
              }
              
              /**
               * @dev Stake tokens for governance and rewards
               */
              function stake(uint256 amount, bool asNodeOperator) external nonReentrant {
                  require(amount > 0, "Amount = 0");
                  require(balanceOf(msg.sender) >= amount, "Insufficient balance");
                  
                  stakes[msg.sender] = Stake({
                      amount: amount,
                      startTime: block.timestamp,
                      multiplier: asNodeOperator ? 200 : 150,  // 2x for nodes, 1.5x for regular
                      isNodeOperator: asNodeOperator
                  });
                  
                  _transfer(msg.sender, address(this), amount);
                  emit TokensStaked(msg.sender, amount);
              }
              
              // Additional functions for governance, rewards, and network operations...
          }


### RESTFul API Tutorial (Not Yet Public Only Example)
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



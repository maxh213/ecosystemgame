# Product Requirements Document: CubeLife Arena
## A Persistent World AI Creature Simulation with Predictive Betting

### Executive Summary

CubeLife Arena is a groundbreaking web-based persistent world simulation game that combines artificial life evolution, LLM-powered creature behavior, and spectator betting mechanics. Players observe and bet on the outcomes of 1000+ cube-shaped digital creatures living in a shared ecosystem, each powered by local AI models through Ollama integration. The game operates on 5-10 minute world ticks, creating a scalable yet engaging experience where evolution, combat, and social interactions unfold in real-time.

### Product Vision and Objectives

**Vision Statement**: Create the world's first massively multiplayer artificial life observatory where AI-driven creatures evolve, compete, and form complex societies while players predict and profit from emergent behaviors.

**Core Objectives**:
1. Demonstrate the potential of LLM-driven game AI at scale
2. Create engaging spectator gameplay through prediction markets
3. Build a self-sustaining ecosystem with genuine emergent behaviors
4. Establish a new genre combining artificial life simulation with betting mechanics
5. Develop using AI-assisted coding tools for rapid iteration

**Unique Value Proposition**: Unlike traditional games, CubeLife Arena treats players as scientists and gamblers observing a genuine artificial ecosystem where every creature's behavior emerges from AI decision-making rather than scripted actions.

### Target Audience

**Primary Audience**:
- **AI Enthusiasts** (25-45): Fascinated by artificial intelligence and emergent behaviors
- **Simulation Game Players**: Fans of games like The Sims, Spore, and Species: ALRE
- **Betting/Prediction Market Users**: SaltyBet viewers and prediction market participants
- **Stream Viewers**: Twitch/YouTube audiences who enjoy 24/7 streams and passive entertainment

**Secondary Audience**:
- **Indie Game Supporters**: Players seeking unique, experimental gameplay
- **Educators/Researchers**: Using the game to study AI behavior and evolution
- **Casual Mobile Players**: Checking in periodically to observe and bet

### Core Features and Game Mechanics

#### 1. Persistent World Ecosystem

**World Structure**:
- Single shared world instance (200x200 grid)
- Multiple biomes: Grassland, Forest, Desert, Arctic
- Dynamic weather system affecting creature behavior
- Resource nodes that regenerate based on consumption
- Day/night cycles influencing creature activity

**Tick System**:
- World updates every 5-10 minutes
- Creature decisions processed in batches
- Environmental changes calculated per tick
- Resource regeneration and consumption balanced

#### 2. AI-Powered Creatures

**Creature Design**:
- Cube-based procedural generation
- 8-16 voxels per creature with genetic variations
- Color-coded by species and traits
- Visual indicators for health, energy, mood

**LLM Integration**:
- Each creature powered by Ollama-hosted models (Phi-4, Gemma 2)
- Personality traits influence prompt engineering
- Memory system for past experiences
- Social learning from other creatures

**Behavioral Systems**:
- **Basic Needs**: Hunger, energy, safety, social
- **Complex Behaviors**: Territory marking, pack hunting, mating rituals
- **Emergent Actions**: Tool use, communication, alliance formation

#### 3. Evolution and Genetics

**NEAT-Based Evolution**:
- Neural network topology evolves over generations
- Physical traits (size, color, appendages) inherited
- Behavioral tendencies passed to offspring
- Mutation rate increases under environmental stress

**Species Development**:
- Speciation through geographic isolation
- Divergent evolution based on biome adaptation
- Hybrid creatures from cross-species breeding
- Extinction events and population bottlenecks

#### 4. Betting and Prediction Markets

**Betting Types**:
- **Combat Outcomes**: Predict winners of creature battles
- **Survival Challenges**: Bet on which creatures survive environmental events
- **Evolution Milestones**: Predict which species will develop specific traits
- **Population Dynamics**: Bet on species dominance over time

**Virtual Currency System**:
- Starting balance: 1000 CubeCoins
- Minimum bet: 10 CubeCoins
- Bankruptcy protection: 100 CubeCoin bailout
- Premium currency for cosmetic unlocks

**Odds Calculation**:
- Dynamic odds based on creature stats and history
- Community betting influences payouts
- AI analysis provides betting insights
- Historical performance tracking

#### 5. Observer Interface

**Camera System**:
- Free-roam camera with smooth controls
- Creature-following mode
- Cinematic auto-camera for events
- Picture-in-picture for multiple views

**Information Displays**:
- Real-time creature stats overlay
- Population graphs and species distribution
- Phylogenetic tree visualization
- Betting interface with odds display

**Social Features**:
- Global chat with betting reactions
- Creature naming and adoption system
- Screenshot and clip sharing
- Community-created observation journals

### Technical Architecture

#### Backend Architecture

**Core Stack**:
- **Language**: Node.js with TypeScript
- **Framework**: FastAPI for API endpoints
- **Real-time**: Socket.IO for WebSocket connections
- **Database**: PostgreSQL with JSONB for flexible creature data
- **Cache**: Redis for session management and real-time data
- **Message Queue**: RabbitMQ for async creature processing

**Entity Component System (ECS)**:
```javascript
class EntityManager {
  entities: Map<UUID, Entity>
  components: Map<ComponentType, Map<UUID, Component>>
  systems: System[]
  
  update(deltaTime: number) {
    for (const system of this.systems) {
      system.process(this.queryEntities(system.requiredComponents))
    }
  }
}
```

**Ollama Integration Architecture**:
```javascript
class CreatureAIManager {
  ollamaClient: OllamaClient
  decisionQueue: PriorityQueue<CreatureDecision>
  
  async processCreatureDecisions() {
    const batch = await this.decisionQueue.getBatch(8)
    const decisions = await this.ollamaClient.batchInference(batch)
    return this.validateAndApplyDecisions(decisions)
  }
}
```

#### Frontend Architecture

**Rendering Stack**:
- **Engine**: Three.js for WebGL rendering
- **UI Framework**: React with MobX for state management
- **Styling**: Tailwind CSS for responsive design
- **Build Tool**: Vite for fast development

**Performance Optimizations**:
- Instanced rendering for 1000+ creatures
- Level-of-detail (LOD) system
- Frustum culling
- Texture atlasing for creature variations

#### Scalability Design

**Horizontal Scaling**:
- Microservice architecture for different systems
- Load balancer for Ollama instances
- Database read replicas
- CDN for static assets

**Performance Targets**:
- Support 1000+ concurrent creatures
- 100-500 simultaneous observers
- <100ms UI response time
- 5-minute tick processing under 30 seconds

### Visual Design Requirements

#### Art Direction

**Visual Style**:
- Minimalist voxel art inspired by Crossy Road
- Vibrant color palette with species differentiation
- Clean, readable UI with gaming aesthetics
- Smooth animations despite cube constraints

**Creature Design System**:
- Base cube body (1-3 segments)
- Procedural appendages (0-6 limbs)
- Eye placement indicating personality
- Particle effects for abilities

**Environment Design**:
- Low-poly terrain with clear biome boundaries
- Stylized vegetation and landmarks
- Dynamic lighting with day/night cycles
- Weather effects (rain, snow, sandstorms)

#### User Interface

**HUD Layout**:
- Minimal overlay during observation
- Expandable panels for detailed information
- Context-sensitive tooltips
- Mobile-responsive design

**Key Screens**:
- Main observation view
- Betting interface modal
- Creature detail panel
- Evolution tree visualization
- Statistics dashboard

### Monetization Strategy

#### Free-to-Play Model

**Core Monetization**:
1. **Premium Currency**: CubeGems for cosmetic purchases
2. **Battle Pass**: Seasonal rewards for active observers
3. **VIP Subscription**: Enhanced betting analytics and exclusive cameras
4. **Cosmetic Items**: Creature accessories, camera filters, UI themes

**Ethical Considerations**:
- No pay-to-win mechanics
- Betting uses only virtual currency
- Clear odds and probability displays
- Responsible gaming features

### Development Roadmap

#### Phase 1: Foundation (Weeks 1-4)
- Core ECS architecture implementation
- Basic creature AI with Ollama integration
- Simple ecosystem with resource system
- WebSocket infrastructure

#### Phase 2: Core Gameplay (Weeks 5-8)
- Evolution and genetics system
- Combat and interaction mechanics
- Betting system implementation
- Observer camera controls

#### Phase 3: Polish and Features (Weeks 9-12)
- Advanced AI behaviors
- Full biome implementation
- Social features and chat
- Performance optimization

#### Phase 4: Beta Launch (Weeks 13-16)
- Closed beta with 100 players
- Load testing and optimization
- Balancing and tuning
- Community feedback integration

### Success Metrics

#### Technical KPIs
- 99.5% uptime
- <500ms decision latency
- 60 FPS client performance
- <5% creature behavior errors

#### Engagement Metrics
- 30-day retention rate >40%
- Average session length >20 minutes
- Daily active users >1000
- Betting participation rate >60%

#### Business Metrics
- 5% conversion to premium
- $10 average revenue per paying user
- 50,000 registered users in 6 months
- Break-even within 12 months

### Risk Mitigation

#### Technical Risks
- **LLM Performance**: Implement caching and fallback behaviors
- **Scalability Issues**: Use progressive loading and LOD systems
- **Creature Behavior Bugs**: Comprehensive testing and gradual rollout

#### Business Risks
- **Gambling Regulations**: Ensure virtual-only currency compliance
- **Player Retention**: Regular content updates and events
- **Competition**: Focus on unique AI-driven gameplay

### Development Guidelines

#### AI-Assisted Development
- Modular architecture for AI tool compatibility
- Comprehensive documentation and comments
- Test-driven development approach
- Clear separation of concerns

#### Code Organization
```
/src
  /client
    /components
    /rendering
    /state
  /server
    /creatures
    /ecosystem
    /betting
    /ai-integration
  /shared
    /types
    /utils
```

### Conclusion

CubeLife Arena represents a unique convergence of artificial life simulation, AI technology, and social betting mechanics. By leveraging cutting-edge LLM integration and proven game design patterns, this project has the potential to create an entirely new genre of observational gameplay. The technical architecture supports massive scale while maintaining engaging moment-to-moment gameplay through emergent AI behaviors and community-driven betting markets.

The emphasis on AI-assisted development ensures rapid iteration and feature implementation, while the monetization strategy provides sustainable revenue without compromising the core experience. With careful execution of this PRD, CubeLife Arena can become a landmark title in AI-driven gaming and establish a new paradigm for persistent world simulations.
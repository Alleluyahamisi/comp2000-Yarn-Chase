# Animal Grid Game

## How to Compile and Run

This program requires Java 11 or Java 21.

**To compile:**
```bash
javac *.java
```

**To run:**
```bash
java Main
```

## How to Play

1. Click on the brown dog to select it and view available moves (shown as white highlighted squares)
2. Click on any highlighted square to move the dog there
3. Collect the colored balls for different effects:
   - Orange balls: Score points
   - Blue balls: Increased movement range for 3 turns
   - Red balls: Reduced movement range for 3 turns
   - Purple balls: Ability to walk on water for 3 turns
4. The yellow cat and blue bird move automatically using AI strategies
5. The status display at the top shows current effects on each animal

## Features Added to Base Code

I extended the basic grid from our class work by implementing a collectible system with different ball types and a terrain system. The game now includes various terrain types (oceans, forests, deserts, and bridges) that affect movement patterns.

## Object-Oriented Programming Implementation

### Inheritance

I implemented an `Actor` base class that serves as the foundation for all game characters (Dog, Cat, Bird). Each animal inherits common functionality from Actor:
- Location tracking on the grid
- Color properties
- Movement capabilities
- Temporary effect management (buffs and debuffs)

Each subclass extends Actor but maintains unique characteristics. For example, the dog has 3 base movement range and brown coloring, while the cat has 2 movement range and golden coloring, and the bird has 4 movement range with steel blue coloring. Each animal also implements its own `rebuildPolys()` method to create distinct visual appearances.

This inheritance approach eliminates code duplication and provides a consistent interface for all game actors. Adding new animals would only require extending Actor and defining specific attributes and appearance.

### Interfaces

I used multiple interfaces to organize different capabilities within the game:

**PlayerControllable**: Marks actors controlled by the player (currently only the Dog)
**AIControlled**: Identifies AI-controlled actors (Cat and Bird)
**Movable**: Defines movement contracts with required methods
**Item**: Marker interface for collectible objects

These interfaces allow the game logic to handle objects based on their capabilities rather than their specific types. For instance, the Stage class can check `instanceof PlayerControllable` to determine whether an actor should respond to player input.

I also implemented a **MovementStrategy** interface that enables different AI behaviors:
- `ChaseDogStrategy`: Makes the cat pursue the dog
- `RandomWalkStrategy`: Makes the bird move randomly

This design makes it straightforward to modify AI behaviors or add new strategies without changing the actor classes themselves.

### Generics

The most complex implementation is the `TurnQueue<E extends Actor>` class, which is a custom generic class for managing turn order. 

The bounded type parameter `<E extends Actor>` ensures type safety by only allowing Actor objects (or their subclasses) in the queue. This prevents compilation errors and eliminates the need for casting. The queue operates circularly, returning to the first actor after the last one completes their turn.

I also made the class implement `Iterable<E>`, which allows for enhanced for-loop usage if needed. This demonstrates understanding of how generics work with existing Java interfaces.

## Design Benefits

This object-oriented approach provides several advantages:

1. **Inheritance** reduces code duplication and ensures consistent behavior across all actors
2. **Interfaces** create clear contracts and enable polymorphic behavior
3. **Generics** provide compile-time type safety while maintaining code flexibility

The modular design makes it easy to extend the game with new features. Adding new animal types, collectibles, or AI strategies would require minimal changes to existing code, which demonstrates good software design principles.
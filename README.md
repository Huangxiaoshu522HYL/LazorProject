# Lazor Group Project

**Authors: Yilin Huang <yhuang259@jhu.edu>, Zhaoyang Min <zmin6@jhu.edu>**  
**Course: EN.540.635.01.FA24 Software Carpentry**

## How to Use

Place any configuration files in the appropriate folder. You need to create a result folder before running this program main.py.  The output images or logs will be saved to a specified folder ("result"), reflecting the laser paths based on grid configurations.


## Code Architecture

### Class `Lazer`
by Zhaoyang Min
- **Purpose**: Represents an individual laser beam in the simulation, storing its coordinates and directional properties. The `Lazer` class is structured to allow tracking of single and reflected beams.
- **Attributes**:
  - `pos`: Tuple representing the laser's coordinates.
  - `dir`: Tuple indicating the laser's directional vector.
  - `next`: Stores the next `Lazer` instance if the laser continues in a straight path.
  - `reflectnext`: Stores the next `Lazer` instance if the laser reflects off a block.
- **Methods**:
  - `__eq__`: Checks equality between two `Lazer` objects, based on position and direction.
  - `__hash__`: Provides a hash for using `Lazer` objects in sets or as dictionary keys.

### Class `Block`
by Zhaoyang Min
- **Purpose**: Represents a block on the board that interacts with the laser beams. The block’s type determines how it affects incoming lasers (e.g., reflecting, transmitting).
- **Attributes**:
  - `pos`: The block’s position on the board.
  - `type`: The block type, which defines how it interacts with lasers (e.g., "reflective", "absorbing").
- **Methods**:
  - `lazer_output(inputLazer)`: Based on the incoming `Lazer`, this method generates output laser beams according to the block's type, adding new `Lazer` instances to represent each possible outcome.

### Class `Board`
by Yilin Huang
- **Purpose**: The `Board` class represents the grid layout of blocks and manages the lasers within the simulation. It handles the placement of lasers, tracks each laser’s path, and calculates interactions with blocks.
- **Attributes**:
  - `data`: A 2D list representing the board's block layout.
  - `width` & `height`: Dimensions of the board.
  - `target`: Specifies target locations or configurations for laser paths.
  - `start`: Initial list of `Lazer` instances representing starting laser points.
  - `grid`: The full grid layout, with each cell containing a `Block` instance.
  - `pointpassed`: Tracks points visited by lasers.
  - `lazerprocessed`: Stores processed laser instances to prevent duplicate processing.
- **Methods**:
  - `buildlazer()`: Initializes the board's lasers and starts their path calculations.
  - `build_A_lazer(lazer)`: Recursive function to process each `Lazer`, calculating its path based on interactions.
  - `not_valid_lazer(lazer)`: Checks if the laser is within board boundaries.
  - `get_next(lazer)`: Calculates the laser’s next position and direction based on its current location and block interaction.
  - `save_pic(filenmae): Save the output solution picture with legends and Lazer solutions picture into corrected folder. 

### Class `Game`
by Yilin Huang
- **Purpose**: The `Game` class encapsulates the entire simulation round. It manages board configuration, block placements, and laser paths, aiming to find valid paths for lasers to reach target points.
- **Attributes**:
  - `game_name`: Name of the game, matching the configuration or file name.
  - `grid`: Holds grid data for block placements.
  - `blocks`: Available block types and their positions on the board.
  - `lazers`: Initial laser configurations.
  - `targets`: Target points or conditions that lasers should meet.
- **Methods**:
  - `read_bff(name)`: Reads configuration files and initializes the board setup.
  - `get_board_permutations`: Generates all possible board layouts based on block arrangements.
  - `solve`: Calculates and validates laser paths for each board permutation to achieve target configurations.

## How to Speed Up the Code

1. **Optimize Laser Tracking**: By using hashable data structures and efficient data handling (e.g., sets for `lazerprocessed`), unnecessary recalculations are minimized.
2. **Efficient Board Representation**: Reducing board dimensions or using a more compact data structure for `grid` could lower memory overhead.
3. **Batch Image Processing**: If generating multiple output images, process images in batches and leverage the Pillow library’s bulk methods to reduce I/O operations.
4. **Parallelize Simulation**: For complex configurations, consider multi-threading or parallel processing (e.g., `concurrent.futures` library) to simulate multiple board layouts simultaneously.

## Additional Components

- **Image Generation**: Uses the Pillow library to create visual representations of the laser paths based on board layouts and interactions with legends annotations. 

## Configuration Files

If applicable, configuration files (e.g., grid data files) can be placed in a designated folder. These files should define initial board setups, block types, laser start points, and targets.






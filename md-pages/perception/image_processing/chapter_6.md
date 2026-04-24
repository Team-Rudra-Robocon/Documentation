# Model Selection and Training

<sub>**Author**
Girija Kulkarni</sub>


## Architecture Choice

The augmentation pipeline ensured the model would be robust to:

- Varied scroll orientations as Robot-2 approaches from different angles
- Different distances between camera and scrolls
- Minor image quality variations during real-time operation

## Comparative Analysis

### Platform Comparison

| Criterion | Jetson Nano | Raspberry Pi 4 | Integrated AI Camera |
|-----------|-------------|----------------|---------------------|
| Setup Complexity | Medium | Low | High (initial) |
| Runtime Efficiency | High | Medium | Very High |
| Power Consumption | 10-20W | 8-15W | 2-5W |
| Physical Size | Medium | Medium | Very Small |
| Autonomy Level | Medium | Medium | High |
| Debugging Ease | High | High | Medium |
| Cost | Medium | Low | Medium |

## Conclusion

Through careful dataset development, model training, and hardware integration, we have created a reliable perception system that meets the stringent requirements of autonomous robotics competition. The integrated AI camera approach offers particular advantages in power efficiency, system simplicity, and competition compliance, making it the recommended solution for deployment.

Future enhancements may include multi-camera systems for 360-degree coverage, sensor fusion with other modalities (ultrasonic, LiDAR), and adaptive learning capabilities to improve performance during competition rounds.
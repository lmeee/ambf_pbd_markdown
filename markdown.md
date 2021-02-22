# ambf_pbd_markdown
# weekly track

## Winter 2020, Week 6 Feb 15 to Feb 27
- Goal: write method and members for pbd physics which replace cBulletWorld class

  - change cmakelist to include source files
  - construct header file example.h.
  - write example.cpp, an example of a cuboid which is pulled by a constanst external force.
  - apply shapematching constraint and met unstable output.
  - output example
  ```
  iteration #9
  9 th iteration: final position for particle 0 : 1.390e-309 | 7.245e-183 | 1.375e+01 
  9 th iteration: final position for particle 1 : 1.000e+00 | 7.245e-183 | 1.375e+01 
  9 th iteration: final position for particle 2 : 1.000e+00 | 1.000e+00 | 1.375e+01 
  9 th iteration: final position for particle 3 : 1.390e-309 | 1.000e+00 | 1.375e+01 
  9 th iteration: final position for particle 4 : 1.390e-309 | 7.245e-183 | 1.475e+01 
  9 th iteration: final position for particle 5 : 1.000e+00 | 7.245e-183 | 1.475e+01 
  9 th iteration: final position for particle 6 : 1.000e+00 | 1.000e+00 | 1.475e+01 
  9 th iteration: final position for particle 7 : 1.390e-309 | 1.000e+00 | 1.475e+01
  ```
  
  TODO:
    - OOP, divide into classes
    - more constraints
    - visualization
    - import robots (joint constraints)



## Winter 2020, Week 6 Feb 8 to Feb 14

- Goal: create a simple simulation (ex. A bunch of particles) in ambf with PBD. change the physics simulation from BULLET-PHYSICS to PBD. Replace cBulletWorld class with my pbd class. Rewrite method and members in it. 


- Understand from ambf_simulator.cpp, this code create dynamic world (bullet world) 
  ```
  g_afWorld = new afWorld(g_cmdOpts.prepend_namespace);
  ```
  - type Afworld inherited from public cBulletWorld, public afConfigHandler, public afComm
  
- Members in cBulletWorld class:
  - btDiscreteDynamicsWorld
    ```
    //! Bullet dynamics world.
    btDiscreteDynamicsWorld* m_bulletWorld;
    ```
    - btDiscreteDynamicsWorld->btDynamicsWorld->btCollisionWorld
    - Add or remove constraint in line 1100 in afFramework.cpp
    - stepSimulation

  - btBroadphaseInterface
    ```
    //! Bullet broad phase collision detection algorithm.
    btBroadphaseInterface* m_bulletBroadphase; (btBroadphaseInterface.h)
    ```
    - In cBulletWorld

  - btCollisionConfiguration
    ```
    //! Bullet collision configuration.
    btCollisionConfiguration* m_bulletCollisionConfiguration; (btCollisionConfiguration.h)
    ```
    - In cBulletWorld

  - btCollisionDispatcher
    ```
    //! Bullet collision dispatcher.
    btCollisionDispatcher* m_bulletCollisionDispatcher;
    ```
    - btCollisionDispatcher->btDispatcher
    - In cBulletWorld

  - btConstraintSolver
    ```
    //! Bullet physics solver.
    btConstraintSolver* m_bulletSolver;
    ```
    - Q: No cpp file found for this?
    - In cBulletWorld

  - not consider for now
    ```
    //! Bullet Softbody World Info
    btSoftBodyWorldInfo* m_bulletSoftBodyWorldInfo;
    //! Bullet Soft Body Solver
    btSoftBodySolver* m_bulletSoftBodySolver;
    ```

- final goal: PBD framework with
  - rigid body (simulated as a point in previous work) and deformable body, interaction between rigid and deformable bodies (friction, etc).
  - ROS
  - haptics力反馈
  - differentiable


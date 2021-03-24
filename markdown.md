# ambf_pbd_markdown
# weekly track

## Winter 2020, Spring break Mar 22nd to Mar 28th

  - video of PBD single hinge joint with universal robots' viusal links with gravity only. Control the joint angle with a publisher subscribed to '/joint_states'
  - https://drive.google.com/file/d/1m5mbRaobWELTBqNN9SHzzK0xCYiipFVd/view?usp=sharing
  - take delta_x = 0.05s, try h = 0.001s/0.005s/0.01s (num of step = 50/10/5), smaller the h, larger the height when arm can reach when swinging to the other side. 
  - highest radian it could reach 0.001s: 3.12763rad, 0.005s: 3.06064rad, 0.01s: 2.98691rad
  - Next step: add another hinge joint, create comparison with 2D dynamic model


## Winter 2020, Week 10 Mar 15th to Mar 21st 
  - goal: implement ur5 model with 2 hingejoints, complete visualization and compare it with the Newton-euler implementation.

  - Work on friction simulation, complete a basic structure for it.
  - A simple visualization program by communicating with publisher in ROS rviz to move robot. 

## Winter 2020, Week 6 Mar 8st to Mar 14th 

  - It is final week, prepare for exam and project
  - position constraint only simulation (totally 60 frames, interval: 0.05s, each screen every 3 frames take one screenshot for gif )
  - gravity is along -y axis, [0, 10, 0]
  - ![pos](https://user-images.githubusercontent.com/51052629/110712337-e078aa00-81b5-11eb-8fb8-8815c6766713.gif)


  - position constraint an d angular constraint together for hinge joint. To test angular constraint, we add and offset to gravity to let angular constraint adjust according to hinge joint constraint.
  - gravity [2, -10, 0]
  - ![ang](https://user-images.githubusercontent.com/51052629/110713201-5bda5b80-81b6-11eb-83ab-f855d4b42a5b.gif)

  - screenshot of an urdf file of second case
  - In second link, hinge joint will have rpy to be approximately [r_value, 0, 0] with the x axis to be aligned. In the sample urdf, <origin rpy="2.09e+00 1.43e-03 1.10e-03" xyz="1.61e-03 -1.12e+00 -4.97e-01"/>. angular constraint modified the value
  - without angular constraint (not hinge joint)
  - ![3posnoang](https://user-images.githubusercontent.com/51052629/110714451-3e0df600-81b8-11eb-80a2-fcc471761379.png)
  - with angular constraint (hinge joint)
  - ![3ang](https://user-images.githubusercontent.com/51052629/110714452-40705000-81b8-11eb-93d0-4007afc0ac57.png)




## Winter 2020, Week 6 Mar 1st to Mar 7th

  - learn about hinge solver in code and learn about quaternion.
  - implement positional constraint and angular constraint for hinge joint with XPBD
  - solver perform well in first 9 frame, but diverge in some specific case.

  - gif
  ![test](https://user-images.githubusercontent.com/51052629/110669297-0b94d680-8181-11eb-9376-ed1e800779cc.gif)
  - in 10th frame step, solver perform well in beginning step but diverge in the following. In normal case, the vector n(n is the delta x before normalizing) should decrease to a value close to 0 in the process 
  - this cause a large velocity is recorded and use in 11th frame step and result in a large vector n in the first iteration.
  ![Screenshot from 2021-03-09 20-00-48](https://user-images.githubusercontent.com/51052629/110574563-2ed46d00-8112-11eb-8dc2-b9bb66e975ae.png)

  frame 9
  ![Screenshot from 2021-03-08 04-55-05](https://user-images.githubusercontent.com/51052629/110573971-14e65a80-8111-11eb-86ba-43e9d68b8503.png)

  frame 10
  ![Screenshot from 2021-03-08 04-53-47](https://user-images.githubusercontent.com/51052629/110573937-05671180-8111-11eb-9418-8259ecb6efcb.png)
  
  frame 11
  ![Screenshot from 2021-03-08 04-54-03](https://user-images.githubusercontent.com/51052629/110573953-0d26b600-8111-11eb-8c48-95b6ec72ebcb.png)




## Winter 2020, Week 6 Feb 22 to Feb 28
- Goal: Write rigid body PBD with joint constraint (universal constraint and slider constraint) with extend PBD

  - Rigid body class
  - Universal constraint implementation
  - A simulation with 2 rigid bodies connected with universal joint
  - Visualization for every time step with URDF file and ROS rviz
  - Understanding XPBD
  - t = 0*0.05s
  ![image](https://user-images.githubusercontent.com/51052629/109461780-84748f80-7a17-11eb-9c4f-a7482fa8734b.png)

  - t = 30*0.05s
  ![image](https://user-images.githubusercontent.com/51052629/109461872-a241f480-7a17-11eb-84f1-ffee9de73be8.png)


## Winter 2020, Week 6 Feb 15 to Feb 21
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


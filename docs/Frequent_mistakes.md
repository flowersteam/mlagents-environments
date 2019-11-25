# Frequent mistakes

In this part, you can find the common mistakes that you could make in Gym and Unity, and their solutions.

Come back to [home](Home.md)

### Contents

- [The learning brain](#brain)

- [The action in Gym-Unity](#convert)

- [The parameter in Gym-Unity](#result)

- [Next Step](#next_step)

  

## <a name="brain">The learning brain in Unity</a>

When you start an environment, you can encounter this error : `list index out of range` (<span style="color:red">**red block**</span>).

<p align="center">
  <img src="images/gym_brain.png"
       alt="Learning brain error GYM"
       width="100%" border="10" />
</p>

It means that the brain you add in the agent or in the academy is not a **learning brain**, or you don't check `control` in the Unity object academy. To correct this error, verify that the brain used is a `learning brain` and the `control` box is checked : <span style="color:green">**green block**</span>.

<p align="center">
  <img src="images/unity_brain.png"
       alt="Learning brain error Unity"
       width="70%" border="10" />
</p>



## <a name="action">The action in Gym-Unity</a>

Each agent has different actions. The shape and the size of the action vector depend on the brain of the agent. You can encounter this kind of error (<span style="color:rgb(255,230,0)">**Yellow block**</span>) :

<p align="center">
  <img src="images/Actionerror.png"
       alt="Convert to JSON and send the object"
       width="100%" border="10" />
</p>

This error means that the action you send has not the **shape and the size expected by the brain**. If you encounter this error, **check in Unity the size and the shape of your brain or change the action vector send**.



### <a name="result">The parameter in Gym-Unity</a>

Each environment has parameters with different names. If you enter a wrong parameter, you can encounter this message (<span style="color:blue">**blue block**</span>): 

<p align="center">
  <img src="images/Parameter_Error.png"
       alt="Convert to JSON and send the object"
       width="100%" border="10" />
</p>

To correct this error, check the **name of parameter** (uppercase, lowercase and number).



##<a name="next_step">Next Step</a>

Come back to [home](Home.md)


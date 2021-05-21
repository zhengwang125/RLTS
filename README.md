


Run [`rl_main_pg.py`](./online-rlts/rl_main_pg.py), the generated models will be stored in the folder `./save` automatically, and you can pick one model with the best performance on the validation data as your model from them.

```
python rl_main_pg.py
```
Here, we provide an interface [`RL.load(checkpoint)`](./online-rlts/rl_brain.py), and you can load an intermediate model to continu


e the training from the checkpoint, which saves your efforts caused by some unexpected exceptions and no need to train again.
In addition, we implemented an incremental computation for reward update in [`rl_env_inc.py`](./online-rlts/rl_env_inc.py), which offers a very fast efficiency for the training, and you may refer the figure [`inc.png`](./online-rlts/inc.png) to get more details.
After your model is trained, we provide a fast interface called [`quick_time_action(observation)`](./online-rlts/rl_brain.py), which replaces the function of DL tool and implements the NN forward more efficiently.



### Error Measurements
We implemented four mainstream error measurements of trajectory simplification in [`data_utils.py`](./online-rlts/data_utils.py), including SED ([`sed_op`](./online-rlts/data_utils.py), [`sed_error`](./online-rlts/data_utils.py)), PED ([`ped_op`](./online-rlts/data_utils.py), [`ped_error`](./online-rlts/data_utils.py)), DAD ([`dad_op`](./online-rlts/data_utils.py), [`dad_error`](./online-rlts/data_utils.py)), and SAD ([`speed_op`](./online-rlts/data_utils.py), [`speed_error`](./online-rlts/data_utils.py)), where '_op' denotes the error on an anchor segment, and "_error" denotes the error between the orignal trajectory and its simplified trajectory. More details can be found in the paper. The default error measurement is SED, if you want to test more measurements, just simply replace the corresponding function name in [`rl_env_inc.py`](./online-rlts/rl_env_inc.py).

### Visualization

We provide an interface [`data_utils.draw(ori_traj, sim_traj, label='sed')`](./online-rlts/data_utils.py) to visualize the simplified trajectory [`vis.png`](./online-rlts/vis.png), you can also use it to observe the model performance during the training or comment it in the codes for your purpose. Note that this part is supported by matplotlib in Python 3.6.
```
final_error = F.draw(self.ori_traj_set[episode], sim_traj)
```

### Evaluation

You can directly run the [`rl_evaluate.py`](./online-rlts/rl_evaluate.py) once you obtain the trained model.

```
python rl_evaluate.py
```
Similarly, you can set a skipping step `skip_size` to train the RLTS-Skip model, which provides a trade-off between the effectiveness and efficiency.

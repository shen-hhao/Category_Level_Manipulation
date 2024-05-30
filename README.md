# Category Level Manipulation

## Introduction

This repository is the official Pytorch implementation of [Learning Category-Level Generalizable Object Manipulation Policy via Generative Adversarial Self-Imitation Learning from Demonstrations](https://arxiv.org/abs/2203.02107).

## Dependency

Please see [installation](https://github.com/haosulab/ManiSkill#installation) of ManiSkill and [installation](https://github.com/haosulab/ManiSkill-Learn#installation) of ManiSkill-Learn, we build our methods on top of [ManiSkill-Learn](https://github.com/haosulab/ManiSkill-Learn) which is a framework for training agents on [SAPIEN Open-Source Manipulation Skill Challenge](https://sapien.ucsd.edu/challenges/maniskill2021/).

To incorporate this project with ManiSkill benchmark, please first overwrite the original [ManiSkill-Learn](https://github.com/haosulab/ManiSkill-Learn) folder with this one, and then install ManiSkill and ManiSkill-Learn.

## Data

Please download ManiSkill demonstration dataset from [here](https://github.com/haosulab/ManiSkill) and store it in the folder "full_mani_skill_data" as instructed in [ManiSkill-Learn](https://github.com/haosulab/ManiSkill-Learn).


## Training

The training code is provided in [training](training). We give an example of using our methods to train on the "OpenCabinetDoor" environment.

### Main Experiments

Method I (GAIL): run the shell command [scripts/train_rl_agent/run_GAIL_baseline_door.sh](scripts/train_rl_agent/run_GAIL_baseline_door.sh)

Method II (GAIL + Progressive Growing of Discriminator): run the shell command [scripts/train_rl_agent/run_GAIL_progressive_door.sh](scripts/train_rl_agent/run_GAIL_progressive_door.sh)

Method III (GAIL + Self-Imitation Learning from Demonstrations): run the shell command [scripts/train_rl_agent/run_GAIL_GASILfD_door.sh](scripts/train_rl_agent/run_GAIL_GASILfD_door.sh)

Method IV (GAIL + Self-Imitation Learning from demonstrations + CLIB Expert Buffer): run the shell command [scripts/train_rl_agent/run_GAIL_CLIB_door.sh](scripts/train_rl_agent/run_GAIL_CLIB_door.sh)

Method V (GAIL + Progressive Growing of Discriminator + Self-Imitation Learning from demonstrations + CLIB Expert Buffer): run the shell command [scripts/train_rl_agent/run_GAIL_use_all_door.sh](scripts/train_rl_agent/run_GAIL_use_all_door.sh)

### Ablation Study with Additional Dense Reward

SAC: run the shell command [scripts/train_rl_agent/run_SAC_door.sh](scripts/train_rl_agent/run_SAC_door.sh)

GAIL + Dense Reward: first temporarily modify [mani_skill_learn/methods/mfrl/gail.py in line 119](https://github.com/wkwan7/Category_Level_Manipulation/blob/da0c446188de6c3717a038687ca2f594d71a12c6/mani_skill_learn/methods/mfrl/gail.py#L119) and set env_r to 0.5 to enable environmental dense reward. Then run the shell command [scripts/train_rl_agent/run_GAIL_baseline_door.sh](scripts/train_rl_agent/run_GAIL_baseline_door.sh)

Method V + Dense Reward: first temporarily modify [mani_skill_learn/methods/mfrl/gail.py in line 119](https://github.com/wkwan7/Category_Level_Manipulation/blob/da0c446188de6c3717a038687ca2f594d71a12c6/mani_skill_learn/methods/mfrl/gail.py#L119) and set env_r to 0.5 to enable environmental dense reward. Then run the shell command [scripts/train_rl_agent/run_GAIL_use_all_door.sh](scripts/train_rl_agent/run_GAIL_use_all_door.sh)


## Evaluation

The evaluation code for one certain checkpoint is as below. You should modify the config path, work-dir path and the checkpoint path for your own model:
```
python -m tools.run_rl {config_path} --evaluation --gpu-ids=0 \
--work-dir={work-dir_path} \
--resume-from {checkpoint_path} \
--cfg-options "env_cfg.env_name=OpenCabinetDoor-v0" "eval_cfg.num=100" "eval_cfg.num_procs=2" "eval_cfg.use_log=True" "eval_cfg.save_traj=False" "eval_cfg.save_video=True"
```


## Validation

You can either split training dataset to construct validation dataset, or you can submit your solutions on [SAPIEN Open-Source Manipulation Skill Challenge](https://sapien.ucsd.edu/challenges/maniskill2021/) to test the performance.

## Citation

If you find our work useful in your research, please consider citing:
```
@article{shen2022learning,
  title={Learning Category-Level Generalizable Object Manipulation Policy via Generative Adversarial Self-Imitation Learning from Demonstrations},
  author={Shen, Hao and Wan, Weikang and Wang, He},
  journal={arXiv preprint arXiv:2203.02107},
  year={2022}
}
```

## License

 This work and the dataset are licensed under [CC BY-NC 4.0][cc-by-nc].

 [![CC BY-NC 4.0][cc-by-nc-image]][cc-by-nc]

 [cc-by-nc]: https://creativecommons.org/licenses/by-nc/4.0/
 [cc-by-nc-image]: https://licensebuttons.net/l/by-nc/4.0/88x31.png

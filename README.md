# CLARity: Reasoning Consistency Alone Can Teach Reinforced Experts

This repository contains the official implementation of the paper "**CLARity: Reasoning Consistency Alone Can Teach Reinforced Experts**", accepted to the main conference of ACL 2026.

## 🚀 Quick Start

1. Install Verl from Verl ([https://github.com/volcengine/verl](https://github.com/volcengine/verl)). It is recommended to use the Docker image for installation.
2. Place `src/training/stage-2/batch.py` into the `verl/workers/reward_manager` folder, overwriting the existing file.
3. Prepare the training data: Run `src/data_preparation/{jec-qa/medqa-usmle}.py` to convert the data into `.parquet` format.
4. Begin training:

   * **Stage 1**: Modify the training script by setting `custom_reward_function.path=src/training/stage-1/{law/med}_faithfulness_rule.py`, then start training.
   * **Stage 2**:

     1. Modify the training script by setting `custom_reward_function.path=src/training/stage-2/{law/med}_faithfulness_model_batch.py`.
     2. Set `reward_model.reward_manager=batch` in the training script and then start training.

## 📂 Code Structure

* **`data`**:

  * `original_data`: Contains the full original dataset for `jec-qa` and `medqa-usmle`.
  * `reformulated_data`: Contains the augmented data generated using our dynamic data reformulation method.

* **`src/data_preparation`**: Code for data preparation. It converts `.json` format data into `.parquet` format and adds system prompts for use with the Verl framework.

* **`src/data_reformulation`**: Contains the full source code for our dynamic data reformulation method (execution order: concatenate -> polish -> diversify -> aggregate).

* **`src/training`**: Scripts for CLARity training.

  * `stage-1`: Code for the reward function in the stage-1 (refine) phase.
  * `stage-2`: Code for the reward function and reward manager in the stage-2 (monitor) phase.

## 🤝 Citation

If you use this code or find our work helpful, please cite our paper:

```bibtex
@misc{lin2025clarityreasoningconsistencyteach,
      title={CLARity: Reasoning Consistency Alone Can Teach Reinforced Experts}, 
      author={Jiuheng Lin and Cong Jiang and Zirui Wu and Jiarui Sun and Yansong Feng},
      year={2025},
      eprint={2510.09278},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2510.09278}, 
}
```
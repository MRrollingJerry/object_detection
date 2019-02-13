# object_detection

This repository is forked and modified from tensorflow object detection model. 

To run baseline code for the hachathon, you may follow the instruction below:

1) # fork / mirror this repository      
    !!!important: make it as your own private repository and assign right to YITU admin!!! 
    
    fork/mirror https://github.com/Dawdleryang/object_detection.git
    
    ``` bash
    # cd hackathon_sg
    git clone https://github.com/your_own_private_repository 
    ```

2) # environment setttings

    ``` bash
    # activate AWS virtual environment
    source activate tensorflow_p36
    ```

    ``` bash
    # Setup PYTHONPATH
    # cd hackathon_sg/ 
    export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim    
    ```

3) # to generate tfrecord data

    ``` bash
    python script/generate_tfrecord_from_csv.py --image_dir ../input/training/images/ --output_path ../input/yitu --csv_file ../input/training/train_label.csv --validation_set_size 500
    ```

4) # to train the model 

    ``` bash 
    python script/train.py --logtostderr --train_dir=training/baseline/ --pipeline_config_path=training/baseline.config
    ```
   #to visualize the training results
      tensorboard --logdir=training/baseline
     
5) # to eval the trained model 

    ``` bash 
    python script/eval.py --logtostderr --pipeline_config_path=training/baseline.config --checkpoint_dir=training/baseline --eval_dir=training/baseline
    ```
    
   #To visualize the eval results
      tensorboard --logdir=eval/

6) # to export the trained model 

    ``` bash
    python script/export_inference_graph.py --input_type image_tensor --pipeline_config_path training/baseline.config   --trained_checkpoint_prefix training/baseline/model.ckpt-20000 --output_directory output/
    ```
    
7) # to output the results to .csv

    ``` bash
    python script/output_csv_results.py threshold=0.5 data_path=../input/testing/images/ model_path=output/frozen_inference_graph.pb output_path=output/submission.csv label_map=../input/label_map.pbtxt
    ```
        
8) # to submit the results 
    please follow the instruction from ”Hackathon Infra User Manual“ to submit your detection results. 

    !!!DO PUSH YOUR CODES FOR EVERY SUBMISSION YOU MADE FOR CODE VERIFICATION PURPOSE!!!



    
 

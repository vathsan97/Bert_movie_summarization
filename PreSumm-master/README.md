
#### Run following commands from /proj/sund778/work/bert_movies/PreSumm/src
####  Step 1. Pretrain on CNN DailyMail data
```
python train.py -mode train -accum_count 5 -batch_size 100 -bert_data_path ../../bert_data_cnndm_final/ -dec_dropout 0.1 -log_file ../../logs/cnndm_baseline -lr 0.1 -model_path ../../model_check/ -save_checkpoint_steps 5000 -seed 777 -sep_optim false -train_steps 200000 -use_bert_emb true -use_interval true -warmup_steps 100  -visible_gpus 0 -max_pos 512 -report_every 50 -enc_hidden_size 512  -enc_layers 6 -enc_ff_size 2048 -enc_dropout 0.1 -dec_layers 6 -dec_hidden_size 512 -dec_ff_size 2048 -encoder baseline -task abs
```

####  Step 2. Train Movie data

```
python train.py -mode train -accum_count 5 -batch_size 100 -bert_data_path ../../bert_data_bin/ -dec_dropout 0.1 -log_file ../../logs/cnndm_moviedata -lr 0.1 -model_path ../../model_check/ -save_checkpoint_steps 5000 -seed 777 -sep_optim false -train_steps 20000 -use_bert_emb true -use_interval true -warmup_steps 100  -visible_gpus 3 -max_pos 512 -report_every 50 -enc_hidden_size 512  -enc_layers 6 -enc_ff_size 2048 -enc_dropout 0.1 -dec_layers 6 -dec_hidden_size 512 -dec_ff_size 2048 -encoder baseline -task abs -train_from ../../model_check/model_step_200000.pt
```

####  Step 3. Evaluvate on movie data
 
```
python train.py -task abs -mode validate -batch_size 3000 -test_batch_size 500 -bert_data_path ../../bert_data_bin/ -log_file ../logs/val_abs_bert_cnndm_movies1 -model_path ../../model_check/ -sep_optim true -use_interval true -visible_gpus 2 -max_pos 512 -max_length 200 -alpha 0.95 -min_length 50 -result_path ../logs/abs_bert_cnndm_movies1
```


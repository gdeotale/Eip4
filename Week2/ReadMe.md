1) Logs for 20 epochs

Train on 60000 samples, validate on 10000 samples
Epoch 1/20

Epoch 00001: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 24s 392us/step - loss: 0.2677 - acc: 0.8721 - val_loss: 0.0412 - val_acc: 0.9877
Epoch 2/20

Epoch 00002: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 189us/step - loss: 0.2581 - acc: 0.8730 - val_loss: 0.0265 - val_acc: 0.9920
Epoch 3/20

Epoch 00003: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 189us/step - loss: 0.2532 - acc: 0.8758 - val_loss: 0.0277 - val_acc: 0.9918
Epoch 4/20

Epoch 00004: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 187us/step - loss: 0.2528 - acc: 0.8737 - val_loss: 0.0325 - val_acc: 0.9900
Epoch 5/20

Epoch 00005: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 187us/step - loss: 0.2551 - acc: 0.8749 - val_loss: 0.0281 - val_acc: 0.9908
Epoch 6/20

Epoch 00006: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 187us/step - loss: 0.2508 - acc: 0.8751 - val_loss: 0.0295 - val_acc: 0.9915
Epoch 7/20

Epoch 00007: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 187us/step - loss: 0.2539 - acc: 0.8735 - val_loss: 0.0302 - val_acc: 0.9912
Epoch 8/20

Epoch 00008: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2453 - acc: 0.8763 - val_loss: 0.0240 - val_acc: 0.9920
Epoch 9/20

Epoch 00009: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2516 - acc: 0.8745 - val_loss: 0.0297 - val_acc: 0.9915
Epoch 10/20

Epoch 00010: LearningRateScheduler setting learning rate to 0.1.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2432 - acc: 0.8774 - val_loss: 0.0311 - val_acc: 0.9907
Epoch 11/20

Epoch 00011: LearningRateScheduler setting learning rate to 0.05.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2351 - acc: 0.8789 - val_loss: 0.0309 - val_acc: 0.9916
Epoch 12/20

Epoch 00012: LearningRateScheduler setting learning rate to 0.05.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2354 - acc: 0.8784 - val_loss: 0.0219 - val_acc: 0.9936
Epoch 13/20

Epoch 00013: LearningRateScheduler setting learning rate to 0.05.
60000/60000 [==============================] - 11s 185us/step - loss: 0.2309 - acc: 0.8809 - val_loss: 0.0162 - val_acc: 0.9951
Epoch 14/20

Epoch 00014: LearningRateScheduler setting learning rate to 0.05.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2293 - acc: 0.8806 - val_loss: 0.0180 - val_acc: 0.9945
Epoch 15/20

Epoch 00015: LearningRateScheduler setting learning rate to 0.05.
60000/60000 [==============================] - 11s 189us/step - loss: 0.2298 - acc: 0.8804 - val_loss: 0.0200 - val_acc: 0.9940
Epoch 16/20

Epoch 00016: LearningRateScheduler setting learning rate to 0.01.
60000/60000 [==============================] - 11s 185us/step - loss: 0.2280 - acc: 0.8799 - val_loss: 0.0164 - val_acc: 0.9949
Epoch 17/20

Epoch 00017: LearningRateScheduler setting learning rate to 0.01.
60000/60000 [==============================] - 11s 185us/step - loss: 0.2263 - acc: 0.8816 - val_loss: 0.0156 - val_acc: 0.9950
Epoch 18/20

Epoch 00018: LearningRateScheduler setting learning rate to 0.01.
60000/60000 [==============================] - 11s 185us/step - loss: 0.2267 - acc: 0.8795 - val_loss: 0.0150 - val_acc: 0.9952
Epoch 19/20

Epoch 00019: LearningRateScheduler setting learning rate to 0.01.
60000/60000 [==============================] - 11s 185us/step - loss: 0.2255 - acc: 0.8800 - val_loss: 0.0161 - val_acc: 0.9945
Epoch 20/20

Epoch 00020: LearningRateScheduler setting learning rate to 0.01.
60000/60000 [==============================] - 11s 186us/step - loss: 0.2250 - acc: 0.8781 - val_loss: 0.0157 - val_acc: 0.9954
<keras.callbacks.History at 0x7f5c6fd75f60>


2) Result of your model.evaluate (on test data)

[0.01566029984247398, 0.9954]

3) Strategy you have taken to achieve the said results

Apart from model described in EIGHTH.ipynb
Change1:
This change results in reduction of parameters from 
Total params: 16,604
Trainable params: 16,360
to
Total params: 13,738
Trainable params: 13,526
Non-trainable params: 212

Changed this
model.add(Convolution2D(32, 3, 3, activation='relu')) #24
model.add(BatchNormalization())
model.add(Dropout(0.1))
model.add(Convolution2D(10, 1, 1, activation='relu')) #22
model.add(MaxPooling2D(pool_size=(2, 2)))#11

to this
model.add(Convolution2D(16, 3, 3, activation='relu')) #24
model.add(BatchNormalization())
model.add(Dropout(0.2))
model.add(MaxPooling2D(pool_size=(2, 2)))#12
model.add(Convolution2D(8, 1, 1, activation='relu')) #22

Change 2:
Increased Dropout rate to 0.2 from 0.1
this was done primarily to reduce overfitting and train fast with increased learning rate described in point 3

Change 3:
Change learning rate from
def scheduler(epoch, lr):
  return round(0.003 * 1/(1 + 0.319 * epoch), 10)
to
def scheduler(epoch, lr):
  if epoch<10:
     return 0.1
  elif epoch<15:
    return 0.05
  else:
    return 0.01
as we have increase dropout rate we need fast learning to matchup with accuracy, so i simply replaced rule based 
learning to constant learning for different epochs.
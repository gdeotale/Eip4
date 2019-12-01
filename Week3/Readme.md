1. Final Validation accuracy for Base Network
Epoch 00046: LearningRateScheduler setting learning rate to 0.0325626832.
390/390 [==============================] - 32s 82ms/step - loss: 0.4780 - acc: 0.8333 - val_loss: 0.4863 - val_acc: 0.8343
Epoch 47/50

2. Your model definition (model.add... ) with output channel size and receptive field
model1 = Sequential()
model1.add(SeparableConvolution2D(filters = 48, kernel_size=(3, 3), 
           strides = (1,1), depth_multiplier = 1,
            input_shape = (32,32,3))) #Receptive Field = 3x3     #output=(32+2*0-3)+1=30
model1.add(BatchNormalization())   #Receptive Field = 3x3     #output=(32+2*0-3)+1=30
model1.add(Activation('relu'))    #Receptive Field = 3x3     #output=(32+2*0-3)+1=30
model1.add(SeparableConvolution2D(96, (3, 3), use_bias=False)) #Receptive field = 5x5 #output=(30+2*0-3)+1=28
model1.add(BatchNormalization()) #Receptive field = 5x5 #output=(30+2*0-3)+1=28
model1.add(Activation('relu')) #Receptive field = 5x5 #output=(30+2*0-3)+1=28
model1.add(SeparableConvolution2D(96, (3, 3), padding='same', use_bias=False)) #Receptive field = 7x7 #output=(30+2*1-3)+1=28
model1.add(BatchNormalization()) #Receptive field = 7x7 #output=(30+2*1-3)+1=28
model1.add(Activation('relu')) #Receptive field = 7x7 #output=(30+2*1-3)+1=28
model1.add(SeparableConvolution2D(192, (3, 3), use_bias=False)) #Receptive field = 9x9 #output=(28+2*0-3)+1=26
model1.add(BatchNormalization()) #Receptive field = 9x9 #output=(28+2*0-3)+1=26
model1.add(Activation('relu')) #Receptive field = 9x9 #output=(28+2*0-3)+1=26
model1.add(Dropout(0.25)) #Receptive field = 9x9 #output=(28+2*0-3)+1=26
model1.add(SeparableConvolution2D(48, (1, 1), use_bias=False)) #Receptive field = 9x9 #output=(26+2*0-1)+1=26

model1.add(MaxPooling2D(pool_size=(2, 2))) #Receptive field = 10x10 #output=(26+2*1-2)/2 +1 = 13 

model1.add(SeparableConvolution2D(48, (3, 3), use_bias=False)) #Receptive field = 14x14 #output=(13+2*0-3)+1=11
model1.add(BatchNormalization()) #Receptive field = 14x14 #output=(13+2*0-3)+1=11
model1.add(Activation('relu')) #Receptive field = 14x14 #output=(13+2*0-3)+1=11
model1.add(SeparableConvolution2D(96, (3, 3), use_bias=False)) #Receptive field = 18x18 #output=(11+2*0-3)+1=9
model1.add(BatchNormalization()) #Receptive field = 18x18 #output=(11+2*0-3)+1=9
model1.add(Activation('relu')) #Receptive field = 18x18 #output=(11+2*0-3)+1=9
model1.add(SeparableConvolution2D(96, (3, 3), padding='same', use_bias=False)) #Receptive field = 22x22 #output=(9+2*1-3)+1=9
model1.add(BatchNormalization()) #Receptive field = 22x22 #output=(9+2*1-3)+1=9
model1.add(Activation('relu')) #Receptive field = 22x22 #output=(9+2*1-3)+1=9
model1.add(SeparableConvolution2D(192, (3, 3), use_bias=False)) #Receptive field = 26x26 #output=(9+2*0-3)+1=7
model1.add(BatchNormalization()) #Receptive field = 26x26 #output=(9+2*0-3)+1=7
model1.add(Activation('relu')) #Receptive field = 26x26 #output=(9+2*0-3)+1=7
model1.add(Dropout(0.25)) #Receptive field = 26x26 #output=(9+2*0-3)+1=7

model1.add(MaxPooling2D(pool_size=(2, 2))) #Receptive field = 28x28 #output=1+(7-2)/2=3

model1.add(SeparableConvolution2D(num_classes, 3, 3)) 
model1.add(BatchNormalization())
#model1.add(Dropout(0.25))

model1.add(Flatten())
model1.add(Activation('softmax'))

# Compile the model
model1.compile(optimizer='adam', loss='categorical_crossentropy', metrics=['accuracy'])

from keras.preprocessing.image import ImageDataGenerator
from keras.callbacks import LearningRateScheduler
############Added augmentation here
datagen = ImageDataGenerator(zoom_range=0.1, 
                             rotation_range=15,
                 width_shift_range=0.1, height_shift_range=0.1,
                 horizontal_flip=True)

def scheduler(epoch, lr):
  return round(0.5 * 1/(1 + 0.319 * epoch), 10)

# Train the model   
############ Added scheduler here
model_info = model1.fit_generator(datagen.flow(train_features, train_labels, batch_size = 128),
                                 samples_per_epoch = train_features.shape[0], nb_epoch = 50, 
                                 validation_data = (test_features, test_labels), verbose=1,
                                  callbacks=[LearningRateScheduler(scheduler, verbose=1)])
end = time.time()
print ("Model took %0.2f seconds to train"%(end - start))
# plot model history
plot_model_history(model_info)
# compute test accuracy
print ("Accuracy on test data is: %0.2f"%accuracy(test_features, test_labels, model1))

3. Your 50 epoch logs

/usr/local/lib/python3.6/dist-packages/ipykernel_launcher.py:30: UserWarning: The semantics of the Keras 2 argument `steps_per_epoch` is not the same as the Keras 1 argument `samples_per_epoch`. `steps_per_epoch` is the number of batches to draw from the generator at each epoch. Basically steps_per_epoch = samples_per_epoch/batch_size. Similarly `nb_val_samples`->`validation_steps` and `val_samples`->`steps` arguments have changed. Update your method calls accordingly.
/usr/local/lib/python3.6/dist-packages/ipykernel_launcher.py:30: UserWarning: Update your `fit_generator` call to the Keras 2 API: `fit_generator(<keras_pre..., validation_data=(array([[[..., verbose=1, callbacks=[<keras.ca..., steps_per_epoch=390, epochs=50)`
Epoch 1/50

Epoch 00001: LearningRateScheduler setting learning rate to 0.5.
390/390 [==============================] - 41s 104ms/step - loss: 1.7550 - acc: 0.3471 - val_loss: 4.9031 - val_acc: 0.2188
Epoch 2/50

Epoch 00002: LearningRateScheduler setting learning rate to 0.3790750569.
390/390 [==============================] - 32s 82ms/step - loss: 1.4327 - acc: 0.4762 - val_loss: 2.8893 - val_acc: 0.3499
Epoch 3/50

Epoch 00003: LearningRateScheduler setting learning rate to 0.3052503053.
390/390 [==============================] - 32s 82ms/step - loss: 1.2531 - acc: 0.5467 - val_loss: 1.5718 - val_acc: 0.4985
Epoch 4/50

Epoch 00004: LearningRateScheduler setting learning rate to 0.2554931017.
390/390 [==============================] - 32s 82ms/step - loss: 1.1321 - acc: 0.5946 - val_loss: 1.4269 - val_acc: 0.5404
Epoch 5/50

Epoch 00005: LearningRateScheduler setting learning rate to 0.2196836555.
390/390 [==============================] - 32s 82ms/step - loss: 1.0511 - acc: 0.6261 - val_loss: 1.2985 - val_acc: 0.5561
Epoch 6/50

Epoch 00006: LearningRateScheduler setting learning rate to 0.1926782274.
390/390 [==============================] - 32s 82ms/step - loss: 0.9858 - acc: 0.6489 - val_loss: 1.5410 - val_acc: 0.4849
Epoch 7/50

Epoch 00007: LearningRateScheduler setting learning rate to 0.1715854496.
390/390 [==============================] - 32s 82ms/step - loss: 0.9358 - acc: 0.6667 - val_loss: 1.1392 - val_acc: 0.6025
Epoch 8/50

Epoch 00008: LearningRateScheduler setting learning rate to 0.1546551191.
390/390 [==============================] - 32s 82ms/step - loss: 0.9008 - acc: 0.6821 - val_loss: 0.9572 - val_acc: 0.6613
Epoch 9/50

Epoch 00009: LearningRateScheduler setting learning rate to 0.1407657658.
390/390 [==============================] - 32s 82ms/step - loss: 0.8583 - acc: 0.6957 - val_loss: 1.0273 - val_acc: 0.6428
Epoch 10/50

Epoch 00010: LearningRateScheduler setting learning rate to 0.1291655903.
390/390 [==============================] - 32s 81ms/step - loss: 0.8313 - acc: 0.7076 - val_loss: 0.8423 - val_acc: 0.7066
Epoch 11/50

Epoch 00011: LearningRateScheduler setting learning rate to 0.1193317422.
390/390 [==============================] - 32s 82ms/step - loss: 0.8045 - acc: 0.7161 - val_loss: 0.8648 - val_acc: 0.7006
Epoch 12/50

Epoch 00012: LearningRateScheduler setting learning rate to 0.1108893324.
390/390 [==============================] - 32s 82ms/step - loss: 0.7823 - acc: 0.7239 - val_loss: 0.8240 - val_acc: 0.7037
Epoch 13/50

Epoch 00013: LearningRateScheduler setting learning rate to 0.1035625518.
390/390 [==============================] - 32s 82ms/step - loss: 0.7554 - acc: 0.7328 - val_loss: 0.7014 - val_acc: 0.7597
Epoch 14/50

Epoch 00014: LearningRateScheduler setting learning rate to 0.0971439674.
390/390 [==============================] - 32s 81ms/step - loss: 0.7365 - acc: 0.7412 - val_loss: 0.7500 - val_acc: 0.7397
Epoch 15/50

Epoch 00015: LearningRateScheduler setting learning rate to 0.0914745701.
390/390 [==============================] - 32s 82ms/step - loss: 0.7172 - acc: 0.7486 - val_loss: 0.8699 - val_acc: 0.7084
Epoch 16/50

Epoch 00016: LearningRateScheduler setting learning rate to 0.0864304235.
390/390 [==============================] - 32s 81ms/step - loss: 0.7017 - acc: 0.7538 - val_loss: 0.6771 - val_acc: 0.7653
Epoch 17/50

Epoch 00017: LearningRateScheduler setting learning rate to 0.0819134993.
390/390 [==============================] - 32s 82ms/step - loss: 0.6849 - acc: 0.7629 - val_loss: 0.8518 - val_acc: 0.7031
Epoch 18/50

Epoch 00018: LearningRateScheduler setting learning rate to 0.0778452437.
390/390 [==============================] - 32s 82ms/step - loss: 0.6717 - acc: 0.7649 - val_loss: 0.7642 - val_acc: 0.7377
Epoch 19/50

Epoch 00019: LearningRateScheduler setting learning rate to 0.0741619697.
390/390 [==============================] - 32s 82ms/step - loss: 0.6568 - acc: 0.7699 - val_loss: 0.7495 - val_acc: 0.7421
Epoch 20/50

Epoch 00020: LearningRateScheduler setting learning rate to 0.0708114998.
390/390 [==============================] - 32s 82ms/step - loss: 0.6435 - acc: 0.7770 - val_loss: 0.7513 - val_acc: 0.7246
Epoch 21/50

Epoch 00021: LearningRateScheduler setting learning rate to 0.0677506775.
390/390 [==============================] - 32s 81ms/step - loss: 0.6328 - acc: 0.7778 - val_loss: 0.7817 - val_acc: 0.7343
Epoch 22/50

Epoch 00022: LearningRateScheduler setting learning rate to 0.0649434992.
390/390 [==============================] - 32s 82ms/step - loss: 0.6192 - acc: 0.7823 - val_loss: 0.6515 - val_acc: 0.7778
Epoch 23/50

Epoch 00023: LearningRateScheduler setting learning rate to 0.0623596907.
390/390 [==============================] - 32s 82ms/step - loss: 0.6099 - acc: 0.7857 - val_loss: 0.5990 - val_acc: 0.7954
Epoch 24/50

Epoch 00024: LearningRateScheduler setting learning rate to 0.0599736116.
390/390 [==============================] - 32s 82ms/step - loss: 0.6024 - acc: 0.7910 - val_loss: 0.5626 - val_acc: 0.8128
Epoch 25/50

Epoch 00025: LearningRateScheduler setting learning rate to 0.0577634011.
390/390 [==============================] - 32s 82ms/step - loss: 0.5900 - acc: 0.7919 - val_loss: 0.6529 - val_acc: 0.7718
Epoch 26/50

Epoch 00026: LearningRateScheduler setting learning rate to 0.0557103064.
390/390 [==============================] - 32s 82ms/step - loss: 0.5799 - acc: 0.7972 - val_loss: 0.6015 - val_acc: 0.7907
Epoch 27/50

Epoch 00027: LearningRateScheduler setting learning rate to 0.0537981493.
390/390 [==============================] - 32s 81ms/step - loss: 0.5780 - acc: 0.7981 - val_loss: 0.6302 - val_acc: 0.7803
Epoch 28/50

Epoch 00028: LearningRateScheduler setting learning rate to 0.0520128992.
390/390 [==============================] - 32s 82ms/step - loss: 0.5657 - acc: 0.7997 - val_loss: 0.6671 - val_acc: 0.7678
Epoch 29/50

Epoch 00029: LearningRateScheduler setting learning rate to 0.0503423278.
390/390 [==============================] - 32s 82ms/step - loss: 0.5589 - acc: 0.8035 - val_loss: 0.5475 - val_acc: 0.8111
Epoch 30/50

Epoch 00030: LearningRateScheduler setting learning rate to 0.0487757292.
390/390 [==============================] - 32s 82ms/step - loss: 0.5498 - acc: 0.8092 - val_loss: 0.5867 - val_acc: 0.7983
Epoch 31/50

Epoch 00031: LearningRateScheduler setting learning rate to 0.0473036897.
390/390 [==============================] - 32s 81ms/step - loss: 0.5421 - acc: 0.8086 - val_loss: 0.6273 - val_acc: 0.7803
Epoch 32/50

Epoch 00032: LearningRateScheduler setting learning rate to 0.0459178988.
390/390 [==============================] - 32s 82ms/step - loss: 0.5391 - acc: 0.8110 - val_loss: 0.6006 - val_acc: 0.7929
Epoch 33/50

Epoch 00033: LearningRateScheduler setting learning rate to 0.0446109921.
390/390 [==============================] - 32s 81ms/step - loss: 0.5298 - acc: 0.8165 - val_loss: 0.5519 - val_acc: 0.8092
Epoch 34/50

Epoch 00034: LearningRateScheduler setting learning rate to 0.0433764206.
390/390 [==============================] - 32s 82ms/step - loss: 0.5283 - acc: 0.8157 - val_loss: 0.6044 - val_acc: 0.7911
Epoch 35/50

Epoch 00035: LearningRateScheduler setting learning rate to 0.0422083404.
390/390 [==============================] - 32s 82ms/step - loss: 0.5215 - acc: 0.8183 - val_loss: 0.5958 - val_acc: 0.7968
Epoch 36/50

Epoch 00036: LearningRateScheduler setting learning rate to 0.0411015208.
390/390 [==============================] - 32s 81ms/step - loss: 0.5105 - acc: 0.8222 - val_loss: 0.5029 - val_acc: 0.8272
Epoch 37/50

Epoch 00037: LearningRateScheduler setting learning rate to 0.0400512656.
390/390 [==============================] - 32s 82ms/step - loss: 0.5152 - acc: 0.8193 - val_loss: 0.5361 - val_acc: 0.8183
Epoch 38/50

Epoch 00038: LearningRateScheduler setting learning rate to 0.0390533469.
390/390 [==============================] - 32s 82ms/step - loss: 0.5025 - acc: 0.8260 - val_loss: 0.5384 - val_acc: 0.8129
Epoch 39/50

Epoch 00039: LearningRateScheduler setting learning rate to 0.0381039476.
390/390 [==============================] - 32s 82ms/step - loss: 0.5006 - acc: 0.8244 - val_loss: 0.5425 - val_acc: 0.8185
Epoch 40/50

Epoch 00040: LearningRateScheduler setting learning rate to 0.0371996131.
390/390 [==============================] - 32s 82ms/step - loss: 0.4960 - acc: 0.8259 - val_loss: 0.5436 - val_acc: 0.8137
Epoch 41/50

Epoch 00041: LearningRateScheduler setting learning rate to 0.0363372093.
390/390 [==============================] - 32s 82ms/step - loss: 0.4967 - acc: 0.8261 - val_loss: 0.5417 - val_acc: 0.8125
Epoch 42/50

Epoch 00042: LearningRateScheduler setting learning rate to 0.0355138859.
390/390 [==============================] - 32s 82ms/step - loss: 0.4884 - acc: 0.8297 - val_loss: 0.5266 - val_acc: 0.8224
Epoch 43/50

Epoch 00043: LearningRateScheduler setting learning rate to 0.0347270454.
390/390 [==============================] - 32s 82ms/step - loss: 0.4938 - acc: 0.8275 - val_loss: 0.5038 - val_acc: 0.8248
Epoch 44/50

Epoch 00044: LearningRateScheduler setting learning rate to 0.0339743154.
390/390 [==============================] - 32s 81ms/step - loss: 0.4803 - acc: 0.8341 - val_loss: 0.5063 - val_acc: 0.8266
Epoch 45/50

Epoch 00045: LearningRateScheduler setting learning rate to 0.0332535249.
390/390 [==============================] - 32s 82ms/step - loss: 0.4813 - acc: 0.8336 - val_loss: 0.5766 - val_acc: 0.8019
Epoch 46/50

Epoch 00046: LearningRateScheduler setting learning rate to 0.0325626832.
390/390 [==============================] - 32s 82ms/step - loss: 0.4780 - acc: 0.8333 - val_loss: 0.4863 - val_acc: 0.8343
Epoch 47/50

Epoch 00047: LearningRateScheduler setting learning rate to 0.0318999617.
390/390 [==============================] - 32s 82ms/step - loss: 0.4740 - acc: 0.8341 - val_loss: 0.5637 - val_acc: 0.8046
Epoch 48/50

Epoch 00048: LearningRateScheduler setting learning rate to 0.0312636779.
390/390 [==============================] - 32s 82ms/step - loss: 0.4666 - acc: 0.8378 - val_loss: 0.5155 - val_acc: 0.8204
Epoch 49/50

Epoch 00049: LearningRateScheduler setting learning rate to 0.0306522805.
390/390 [==============================] - 32s 81ms/step - loss: 0.4647 - acc: 0.8371 - val_loss: 0.4851 - val_acc: 0.8342
Epoch 50/50

Epoch 00050: LearningRateScheduler setting learning rate to 0.0300643377.
390/390 [==============================] - 32s 82ms/step - loss: 0.4618 - acc: 0.8398 - val_loss: 0.4824 - val_acc: 0.8335
Model took 1603.67 seconds to train

Accuracy on test data is: 83.35
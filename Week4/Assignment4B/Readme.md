1) Able to reach overall validation accuracy of 88.24

2) Changes made:
   a)  Data Augmentation added : 
      rotation_range=15,
      width_shift_range=0.1,
	  height_shift_range=0.1,
	  zoom_range=0.1,
	  preprocessing_function=get_random_eraser(v_l=0, v_h=1) ##for cut out
   
   b) learning rate changed like this
      if epoch < 5:
        lr = 0.002
    elif epoch < 10:
        lr = 0.001
    elif epoch < 20:
        lr = 0.0005
    elif epoch < 30:
        lr = 0.0001
    elif epoch < 35:
        lr = 0.000075
    elif epoch < 40:
        lr = 0.00005
    elif epoch < 45:
        lr = 0.000025
    else:
        lr = 0.00001
   
   c) kernel_initializer='he_normal' changed to 'glorot_uniform'
	
   d) Didn't changed anything in Architecture of resnet_20v1
	
   e) Added gradcam result for 10 different images at end of .ipynb file

3) Using real-time data augmentation.
Epoch 1/50
Learning rate:  0.002
 - 85s - loss: 1.7022 - acc: 0.4327 - val_loss: 1.6317 - val_acc: 0.5003

Epoch 00001: val_acc improved from -inf to 0.50030, saving model to /content/saved_models/cifar10_ResNet20v1_model.001.h5
Epoch 2/50
Learning rate:  0.002
 - 77s - loss: 1.3723 - acc: 0.5694 - val_loss: 1.3754 - val_acc: 0.5952

Epoch 00002: val_acc improved from 0.50030 to 0.59520, saving model to /content/saved_models/cifar10_ResNet20v1_model.002.h5
Epoch 3/50
Learning rate:  0.002
 - 77s - loss: 1.2405 - acc: 0.6294 - val_loss: 1.2774 - val_acc: 0.6285

Epoch 00003: val_acc improved from 0.59520 to 0.62850, saving model to /content/saved_models/cifar10_ResNet20v1_model.003.h5
Epoch 4/50
Learning rate:  0.002
 - 77s - loss: 1.1680 - acc: 0.6594 - val_loss: 1.2458 - val_acc: 0.6570

Epoch 00004: val_acc improved from 0.62850 to 0.65700, saving model to /content/saved_models/cifar10_ResNet20v1_model.004.h5
Epoch 5/50
Learning rate:  0.002
 - 76s - loss: 1.1169 - acc: 0.6834 - val_loss: 1.1695 - val_acc: 0.6870

Epoch 00005: val_acc improved from 0.65700 to 0.68700, saving model to /content/saved_models/cifar10_ResNet20v1_model.005.h5
Epoch 6/50
Learning rate:  0.001
 - 76s - loss: 0.9759 - acc: 0.7315 - val_loss: 1.0747 - val_acc: 0.7217

Epoch 00006: val_acc improved from 0.68700 to 0.72170, saving model to /content/saved_models/cifar10_ResNet20v1_model.006.h5
Epoch 7/50
Learning rate:  0.001
 - 76s - loss: 0.9292 - acc: 0.7441 - val_loss: 1.0041 - val_acc: 0.7435

Epoch 00007: val_acc improved from 0.72170 to 0.74350, saving model to /content/saved_models/cifar10_ResNet20v1_model.007.h5
Epoch 8/50
Learning rate:  0.001
 - 77s - loss: 0.8956 - acc: 0.7540 - val_loss: 1.0010 - val_acc: 0.7372

Epoch 00008: val_acc did not improve from 0.74350
Epoch 9/50
Learning rate:  0.001
 - 76s - loss: 0.8701 - acc: 0.7608 - val_loss: 0.8008 - val_acc: 0.7905

Epoch 00009: val_acc improved from 0.74350 to 0.79050, saving model to /content/saved_models/cifar10_ResNet20v1_model.009.h5
Epoch 10/50
Learning rate:  0.001
 - 77s - loss: 0.8535 - acc: 0.7661 - val_loss: 1.0252 - val_acc: 0.7282

Epoch 00010: val_acc did not improve from 0.79050
Epoch 11/50
Learning rate:  0.0005
 - 77s - loss: 0.7677 - acc: 0.7942 - val_loss: 0.7863 - val_acc: 0.7945

Epoch 00011: val_acc improved from 0.79050 to 0.79450, saving model to /content/saved_models/cifar10_ResNet20v1_model.011.h5
Epoch 12/50
Learning rate:  0.0005
 - 77s - loss: 0.7416 - acc: 0.8019 - val_loss: 0.7864 - val_acc: 0.7959

Epoch 00012: val_acc improved from 0.79450 to 0.79590, saving model to /content/saved_models/cifar10_ResNet20v1_model.012.h5
Epoch 13/50
Learning rate:  0.0005
 - 77s - loss: 0.7266 - acc: 0.8050 - val_loss: 0.6773 - val_acc: 0.8249

Epoch 00013: val_acc improved from 0.79590 to 0.82490, saving model to /content/saved_models/cifar10_ResNet20v1_model.013.h5
Epoch 14/50
Learning rate:  0.0005
 - 76s - loss: 0.7094 - acc: 0.8105 - val_loss: 0.7499 - val_acc: 0.8026

Epoch 00014: val_acc did not improve from 0.82490
Epoch 15/50
Learning rate:  0.0005
 - 76s - loss: 0.7008 - acc: 0.8118 - val_loss: 0.7449 - val_acc: 0.8022

Epoch 00015: val_acc did not improve from 0.82490
Epoch 16/50
Learning rate:  0.0005
 - 76s - loss: 0.6890 - acc: 0.8159 - val_loss: 0.6685 - val_acc: 0.8240

Epoch 00016: val_acc did not improve from 0.82490
Epoch 17/50
Learning rate:  0.0005
 - 76s - loss: 0.6770 - acc: 0.8186 - val_loss: 0.7702 - val_acc: 0.8013

Epoch 00017: val_acc did not improve from 0.82490
Epoch 18/50
Learning rate:  0.0005
 - 76s - loss: 0.6664 - acc: 0.8223 - val_loss: 0.6626 - val_acc: 0.8361

Epoch 00018: val_acc improved from 0.82490 to 0.83610, saving model to /content/saved_models/cifar10_ResNet20v1_model.018.h5
Epoch 19/50
Learning rate:  0.0005
 - 76s - loss: 0.6582 - acc: 0.8245 - val_loss: 0.7298 - val_acc: 0.8114

Epoch 00019: val_acc did not improve from 0.83610
Epoch 20/50
Learning rate:  0.0005
 - 76s - loss: 0.6515 - acc: 0.8261 - val_loss: 0.7538 - val_acc: 0.8028

Epoch 00020: val_acc did not improve from 0.83610
Epoch 21/50
Learning rate:  0.0001
 - 76s - loss: 0.5934 - acc: 0.8449 - val_loss: 0.5507 - val_acc: 0.8632

Epoch 00021: val_acc improved from 0.83610 to 0.86320, saving model to /content/saved_models/cifar10_ResNet20v1_model.021.h5
Epoch 22/50
Learning rate:  0.0001
 - 76s - loss: 0.5715 - acc: 0.8514 - val_loss: 0.5623 - val_acc: 0.8625

Epoch 00022: val_acc did not improve from 0.86320
Epoch 23/50
Learning rate:  0.0001
 - 76s - loss: 0.5612 - acc: 0.8549 - val_loss: 0.5648 - val_acc: 0.8625

Epoch 00023: val_acc did not improve from 0.86320
Epoch 24/50
Learning rate:  0.0001
 - 76s - loss: 0.5472 - acc: 0.8580 - val_loss: 0.5568 - val_acc: 0.8643

Epoch 00024: val_acc improved from 0.86320 to 0.86430, saving model to /content/saved_models/cifar10_ResNet20v1_model.024.h5
Epoch 25/50
Learning rate:  0.0001
 - 76s - loss: 0.5481 - acc: 0.8597 - val_loss: 0.5742 - val_acc: 0.8618

Epoch 00025: val_acc did not improve from 0.86430
Epoch 26/50
Learning rate:  0.0001
 - 76s - loss: 0.5399 - acc: 0.8624 - val_loss: 0.5269 - val_acc: 0.8706

Epoch 00026: val_acc improved from 0.86430 to 0.87060, saving model to /content/saved_models/cifar10_ResNet20v1_model.026.h5
Epoch 27/50
Learning rate:  0.0001
 - 76s - loss: 0.5331 - acc: 0.8641 - val_loss: 0.5396 - val_acc: 0.8663

Epoch 00027: val_acc did not improve from 0.87060
Epoch 28/50
Learning rate:  0.0001
 - 76s - loss: 0.5332 - acc: 0.8618 - val_loss: 0.6166 - val_acc: 0.8449

Epoch 00028: val_acc did not improve from 0.87060
Epoch 29/50
Learning rate:  0.0001
 - 76s - loss: 0.5284 - acc: 0.8635 - val_loss: 0.5374 - val_acc: 0.8657

Epoch 00029: val_acc did not improve from 0.87060
Epoch 30/50
Learning rate:  0.0001
 - 76s - loss: 0.5207 - acc: 0.8672 - val_loss: 0.5208 - val_acc: 0.8703

Epoch 00030: val_acc did not improve from 0.87060
Epoch 31/50
Learning rate:  7.5e-05
 - 76s - loss: 0.5176 - acc: 0.8663 - val_loss: 0.5123 - val_acc: 0.8736

Epoch 00031: val_acc improved from 0.87060 to 0.87360, saving model to /content/saved_models/cifar10_ResNet20v1_model.031.h5
Epoch 32/50
Learning rate:  7.5e-05
 - 76s - loss: 0.5112 - acc: 0.8680 - val_loss: 0.5344 - val_acc: 0.8648

Epoch 00032: val_acc did not improve from 0.87360
Epoch 33/50
Learning rate:  7.5e-05
 - 76s - loss: 0.5064 - acc: 0.8712 - val_loss: 0.5240 - val_acc: 0.8667

Epoch 00033: val_acc did not improve from 0.87360
Epoch 34/50
Learning rate:  7.5e-05
 - 76s - loss: 0.5009 - acc: 0.8712 - val_loss: 0.5254 - val_acc: 0.8702

Epoch 00034: val_acc did not improve from 0.87360
Epoch 35/50
Learning rate:  7.5e-05
 - 76s - loss: 0.5004 - acc: 0.8721 - val_loss: 0.5170 - val_acc: 0.8719

Epoch 00035: val_acc did not improve from 0.87360
Epoch 36/50
Learning rate:  5e-05
 - 76s - loss: 0.4924 - acc: 0.8739 - val_loss: 0.5151 - val_acc: 0.8715

Epoch 00036: val_acc did not improve from 0.87360
Epoch 37/50
Learning rate:  5e-05
 - 76s - loss: 0.4952 - acc: 0.8727 - val_loss: 0.5099 - val_acc: 0.8742

Epoch 00037: val_acc improved from 0.87360 to 0.87420, saving model to /content/saved_models/cifar10_ResNet20v1_model.037.h5
Epoch 38/50
Learning rate:  5e-05
 - 76s - loss: 0.4870 - acc: 0.8743 - val_loss: 0.5093 - val_acc: 0.8725

Epoch 00038: val_acc did not improve from 0.87420
Epoch 39/50
Learning rate:  5e-05
 - 76s - loss: 0.4824 - acc: 0.8753 - val_loss: 0.5062 - val_acc: 0.8732

Epoch 00039: val_acc did not improve from 0.87420
Epoch 40/50
Learning rate:  5e-05
 - 76s - loss: 0.4807 - acc: 0.8773 - val_loss: 0.4906 - val_acc: 0.8808

Epoch 00040: val_acc improved from 0.87420 to 0.88080, saving model to /content/saved_models/cifar10_ResNet20v1_model.040.h5
Epoch 41/50
Learning rate:  2.5e-05
 - 76s - loss: 0.4739 - acc: 0.8785 - val_loss: 0.5024 - val_acc: 0.8748

Epoch 00041: val_acc did not improve from 0.88080
Epoch 42/50
Learning rate:  2.5e-05
 - 76s - loss: 0.4786 - acc: 0.8782 - val_loss: 0.4862 - val_acc: 0.8791

Epoch 00042: val_acc did not improve from 0.88080
Epoch 43/50
Learning rate:  2.5e-05
 - 77s - loss: 0.4750 - acc: 0.8789 - val_loss: 0.4999 - val_acc: 0.8764

Epoch 00043: val_acc did not improve from 0.88080
Epoch 44/50
Learning rate:  2.5e-05
 - 76s - loss: 0.4702 - acc: 0.8805 - val_loss: 0.4957 - val_acc: 0.8780

Epoch 00044: val_acc did not improve from 0.88080
Epoch 45/50
Learning rate:  2.5e-05
 - 76s - loss: 0.4692 - acc: 0.8809 - val_loss: 0.4875 - val_acc: 0.8824

Epoch 00045: val_acc improved from 0.88080 to 0.88240, saving model to /content/saved_models/cifar10_ResNet20v1_model.045.h5
Epoch 46/50
Learning rate:  1e-05
 - 76s - loss: 0.4728 - acc: 0.8796 - val_loss: 0.4881 - val_acc: 0.8801

Epoch 00046: val_acc did not improve from 0.88240
Epoch 47/50
Learning rate:  1e-05
 - 76s - loss: 0.4644 - acc: 0.8821 - val_loss: 0.4869 - val_acc: 0.8813

Epoch 00047: val_acc did not improve from 0.88240
Epoch 48/50
Learning rate:  1e-05
 - 76s - loss: 0.4659 - acc: 0.8812 - val_loss: 0.4865 - val_acc: 0.8811

Epoch 00048: val_acc did not improve from 0.88240
Epoch 49/50
Learning rate:  1e-05
 - 76s - loss: 0.4631 - acc: 0.8840 - val_loss: 0.4864 - val_acc: 0.8815

Epoch 00049: val_acc did not improve from 0.88240
Epoch 50/50
Learning rate:  1e-05
 - 76s - loss: 0.4631 - acc: 0.8836 - val_loss: 0.4882 - val_acc: 0.8806

Epoch 00050: val_acc did not improve from 0.88240
10000/10000 [==============================] - 2s 209us/step
Test loss: 0.4881829994678497
Test accuracy: 0.8806
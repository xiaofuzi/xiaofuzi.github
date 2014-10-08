---
layout: post
title: Sort study
---


# 插入排序
##基本思想及举例说明

插入排序的基本思想是，将元素逐个添加到已经排序好的数组中去，同时要求，插入的元素必须在正确的位置，这样原来排序好的数组是仍然有序的。

在实际使用中，通常是排序整个无序数组，所以把这个无序数组分为两部分排序好的子数组和待插入的元素。第一轮时，将第一个元素作为排序好的子数组，插入第二个元素；第二轮，将前两个元素作为排序好的数组，插入第三个元素。以此类推，第i轮排序时，在前i个元素的子数组中插入第i+1个元素。直到所有元素都加入排序好数组。

###下面，以对 3  2  4  1 为例
进行选择排序插入过程，使用j记录元素需要插入的位置。排序目标是使数组从小到大排列。

###第1轮
* [ 3 ]  [ 2  4  1 ] （最初状态，将第1个元素分为排序好的子数组，其余为待插入元素）
* [ 3 ]  [ 2  4  1 ]  （由于3>2，所以待插入位置j=1）
* [ 2  3 ]  [ 4  1 ]  （将2插入到位置j）

###第2轮
* [ 2  3 ]  [ 4  1 ] （第1轮排序结果）
* [ 2  3 ]  [ 4  1 ] （由于2<4，所以先假定j=2）
* [ 2  3 ]  [ 4  1 ] （由于3<4，所以j=3）
* [ 2  3  4 ]  [ 1 ] （由于4刚好在位置3，无需插入）

###第3轮
* [ 2  3  4 ]  [ 1 ] （第2轮排序结果）
* [ 2  3  4 ]  [ 1 ] （由于1<2，所以j=1）
* [1  2  3  4 ]    （将1插入位置j，待排序元素为空，排序结束）

###算法总结及实现

选择排序对大小为N的无序数组R[N]进行排序，进行N-1轮选择过程。首先将第1个元素作为已经排序好的子数组，然后将剩余的N-1个元素，逐个插入到已经排序好子数组；。因此，在第 i轮排序时，前i个元素总是有序的，将第i+1个元素插入到正确的位置
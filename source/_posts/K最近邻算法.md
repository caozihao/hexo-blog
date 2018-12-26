---
title: K最近邻算法
date: 2018-12-26 10:12:47
updated:
tags:
- 算法
- K最近邻算法
thumbnail: /images/算法/bg.jpg
---
####  K最近邻算法

    //漫画算法图解 P163页
    // 求估计最近4天卖出面包的数量
    const log = console.log.bind(this);

      const algorithm = (originData,testData)=>{
          let result = [];
          let value = [];
          for(let item of testData){
              for(let key in item){
                  value.push(calculateSimilarNumber(key,originData) );
                  result.push(item[key])
              }
            
          }
          let limitNum = 4;
          let sortArr = bubbleSort(value);
          sortArr = sortArr.splice(0,limitNum);
          let totalNum = sortArr.reduce((total,index)=>{
              return total + result[index];
          },0)
          // log('totalNum ->',totalNum);
          //  log('value ->',value);
          //  log('result ->',result);
          //  log('sortArr ->',sortArr);
          let averageNum = totalNum / limitNum;
          // log('averageNum ->',averageNum);
          return averageNum
      }
          
      const calculateSimilarNumber = (compareData,originData)=>{
          let result = 0;
          if(compareData.length && originData.length){
              let compareDataArr = compareData.split(',');
              let originDataArr = originData.split(',');
              for(let i =0;i < compareDataArr.length;i++){
                  result += Math.pow(compareDataArr[i] - originDataArr[i],2);
              }
              result = Math.round(Math.sqrt(result) * 100) / 100;
          }
          
          return result;
      }

      const bubbleSort = (originArr)=>{
          let arr = [...originArr];
          let sortArr = [];
          for(let i =0;i <arr.length;i++ ){
              sortArr.push(i);
          }
          for(let i = 0; i < arr.length - 1;i++){
              for(let j=0;j < arr.length-i-1;j++){
                  if(arr[j] > arr[j+1]){
                      let temp = arr[j];
                      arr[j] = arr[j+1];
                      arr[j+1] = temp;
                      
                      let temp2 = sortArr[j];
                      sortArr[j] = sortArr[j+1];
                      sortArr[j+1] = temp2;
                  }
              }
          }
          return sortArr;
      }

      const testData = [
          {
              '5,1,0':300
          },
          {
              '3,1,1':225
          },
          {
              '1,1,0':75
          },
          {
              '4,0,1':200
          },
          {
              '4,0,0':150
          },
          {
              '2,0,0':50
          }
      ]

      const originData = '4,1,0';

      algorithm(originData,testData);

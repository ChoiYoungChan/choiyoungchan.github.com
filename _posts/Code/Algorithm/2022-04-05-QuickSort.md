---
title:  "[Sort] QuickSort"
excerpt: Unity에서 사용하는 퀵정렬(QuickSort)

categories:
  - Algorithm
tags:
  - [Algorithm, QuickSort, 퀵 정렬, 정렬]

toc: true
toc_sticky: true
 
date: 2022-04-23
last_modified_at: 2022-04-23
---

## 개요
퀵 정렬(Quick Sort)이란?
=> 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법<br> 

정렬하는 과정
1. 리스트 안의 한 요소를 선택한다. 이때 선택한 원로를 피벗(Pivot)이라한다.
2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로, 큰 요소들은 오른쪽으로 옮겨진다.
3. 피벗을 제외한 왼쪽, 오른쪽 리스트를 위의 과정으로 다시 정렬한다.

<br>

![2022-04-23-QuickSort_006](https://user-images.githubusercontent.com/40765022/164965350-02f0ba7c-a474-47ca-89e0-7ccbbea38e0a.gif)<br>

> (이미지 출처 : https://namu.wiki/w/%EC%A0%95%EB%A0%AC%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98?from=%ED%80%B5%20%EC%A0%95%EB%A0%AC#s-2.2.3)
<br><br>

* 장점
  * 속도가 빠르다.
  * 추가 메모리 공간을 필요로 하지 않는다.

*  단점
   * 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행 시간이 더 많이 걸린다.
 <br>

## 유니티에서 예제
---

### 소스코드
아래는 유니티를 기준으로 작성하였으나 기본적으로 C#이기때문에 숫자를 입력하고 출력하는 부분 외에는 바로 참고하셔도 무방합니다.<br>

[초기화 및 실행함수]<br>
``` C#
#region private
    [SerializeField] InputField m_input_txt;
    [SerializeField] Text m_answer_txt;

    string[] m_split_text;
    string m_input_text, m_output_text;
    List<int> input_txt_split;
#endregion

    public override void Awake()
    {
        m_input_text = null;
        m_output_text = null;

        input_txt_split = new List<int>();
    }

    /// <summary>
    /// active this func When press Enter key
    /// </summary>
    public void OnclickEnter()
    {
        m_input_text = m_input_txt.GetComponent<InputField>().text;

        // split text of inputfield
        m_split_text = m_input_text.Split(',');

        // add splited text into int list(input_txt_split) 
        for (int count = 0; count < m_split_text.Length; count ++) {
            input_txt_split.Add(int.Parse(m_split_text[count]));
        }

        // start Quick Sort
        QuickSort(0, input_txt_split.Count - 1);

        for (int count = 0; count < input_txt_split.Count; count++) {
            m_output_text += input_txt_split[count].ToString() + " ";
        }

        // Display result of QuickSort
        m_answer_txt.text = m_output_text;
    }
```

<br>

[퀵 정렬]<br>
``` C#
    /// <summary>
    /// QuickSort Func
    /// </summary>
    /// <param name="left_num"> left number </param>
    /// <param name="right_num"> right number </param>
    private void QuickSort(int left_num, int right_num)
    {
        if (left_num < right_num) {
            int pivot = Partition(left_num, right_num);
            if (pivot > 1) {
                QuickSort(left_num, pivot - 1);
            }

            if ((pivot + 1) < right_num) {
                QuickSort((pivot + 1), right_num);
            }
        }
    }
```
<br>

[피벗 설정 및 정렬]<br>
``` C#
    /// <summary>
    /// make up pivot and sort
    /// </summary>
    /// <param name="left_num"> left number </param>
    /// <param name="right_num"> right number </param>
    /// <returns></returns>
    private int Partition(int left_num, int right_num)
    {
        int pivot = input_txt_split[left_num];
        while(true) {
            while(input_txt_split[left_num] < pivot) {
                left_num++;
            }
            while(input_txt_split[right_num] > pivot) {
                right_num--;
            }

            if(left_num < right_num) {
                int temp_num = input_txt_split[right_num];
                input_txt_split[right_num] = input_txt_split[left_num];
                input_txt_split[left_num] = temp_num;
            } else {
                return right_num;
            }
        }
    }
```
<br>

[전체 코드]<br>
``` C#
public class QuickSortManager : BaseTemplateClass
{
#region private
    [SerializeField] InputField m_input_txt;
    [SerializeField] Text m_answer_txt;

    string[] m_split_text;
    string m_input_text, m_output_text;
    List<int> input_txt_split;
#endregion

    public override void Awake()
    {
        m_input_text = null;
        m_output_text = null;

        input_txt_split = new List<int>();
    }

    /// <summary>
    /// active this func When press Enter key
    /// </summary>
    public void OnclickEnter()
    {
        m_input_text = m_input_txt.GetComponent<InputField>().text;

        // split text of inputfield
        m_split_text = m_input_text.Split(',');

        // add splited text into int list(input_txt_split) 
        for (int count = 0; count < m_split_text.Length; count ++) {
            input_txt_split.Add(int.Parse(m_split_text[count]));
        }

        // start Quick Sort
        QuickSort(0, input_txt_split.Count - 1);

        for (int count = 0; count < input_txt_split.Count; count++) {
            m_output_text += input_txt_split[count].ToString() + " ";
        }

        // Display result of QuickSort
        m_answer_txt.text = m_output_text;
    }

    /// <summary>
    /// QuickSort Func
    /// </summary>
    /// <param name="left_num"> left number </param>
    /// <param name="right_num"> right number </param>
    private void QuickSort(int left_num, int right_num)
    {
        if (left_num < right_num) {
            int pivot = Partition(left_num, right_num);
            if (pivot > 1) {
                QuickSort(left_num, pivot - 1);
            }

            if ((pivot + 1) < right_num) {
                QuickSort((pivot + 1), right_num);
            }
        }
    }

    /// <summary>
    /// make up pivot and sort
    /// </summary>
    /// <param name="left_num"> left number </param>
    /// <param name="right_num"> right number </param>
    /// <returns></returns>
    private int Partition(int left_num, int right_num)
    {
        int pivot = input_txt_split[left_num];
        while(true) {
            while(input_txt_split[left_num] < pivot) {
                left_num++;
            }
            while(input_txt_split[right_num] > pivot) {
                right_num--;
            }

            if(left_num < right_num) {
                int temp_num = input_txt_split[right_num];
                input_txt_split[right_num] = input_txt_split[left_num];
                input_txt_split[left_num] = temp_num;
            } else {
                return right_num;
            }
        }
    }
}
```
<br>


### 실행 영상
<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Algorithm/Sort/QuickSort_004.mp4" type="video/mp4">
</video>

<br>
<br>

<video width="70%" height="70%" controls="controls">
  <source src="/assets/images/post/Algorithm/Sort/QuickSort_005.mp4" type="video/mp4">
</video>
<br>

[Top](#){: .btn .btn--primary }{: .align-right}
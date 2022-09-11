---
title:  "[Algorithm] SelectSort"
excerpt: Unity에서 사용하는 선택 정렬(SelectSort)

categories:
  - Algorithm
tags:
  - [Algorithm, SelectSort, 선택 정렬, 정렬]

toc: true
toc_sticky: true
 
date: 2022-04-30
last_modified_at: 2022-04-30
---

## 개요
선택 정렬(SelectSort)이란?
=> 해당 순서에 값을 넣을 위치는 이미 정해져 있고, 그 위치에 어떤 값을 넣을지 선택하는 알고리즘<br>

삽입정렬과의 차이점
* 선택정렬 : 배열에서 해당 자리를 이미 선택하고 그 자리에 오는 값을 찾는 것
* 삽입정렬 : 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교하여 자신의 위치를 찾아 삽입하는 것

정렬하는 과정
1. 배열에서 최소값을 찾는다.
2. 최소값이 배열의 맨 앞의 값보다 작으면 자리를 교체한다.
3. 맨 앞의 값를 제외한 1~2 과정을 반복한다.
<br>

![selectionsort](https://user-images.githubusercontent.com/40765022/189513532-3df318bf-e2d7-48e1-b46b-d9c844f8cfec.png)
> (이미지 출처 :https://programmercave0.github.io/blog/2017/08/29/C++-Selection-sort-using-STL)

<br>

* 장점
  * 거품정렬(Bubble sort)과 마찬가지로 알고리즘이 단순합니다.
  * 정렬을 위한 비교 횟수는 많지만, 거품정렬(Bubble Sort)에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적이다.
  * 버블정렬(Bubble Sort)와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식(제자리 정렬, In-place Sort)이므로, 다른 메모리 공간을 필요로 하지 않는다. 

*  단점
   * 시간복잡도가 O(n^2)으로, 비효율적이다.
   * 불안정 정렬(Unstable Sort)이다.
 <br>

## 유니티에서 예제
---

### 소스코드
아래는 유니티를 기준으로 작성하였으나 기본적으로 C#이기때문에 숫자를 입력하고 출력하는 부분 외에는 바로 참고하셔도 무방합니다.<br><br>

[초기화 및 출력함수]<br>
``` C#
#region private
    [SerializeField] InputField m_input_txt;
    [SerializeField] Text m_answer_txt;

    string[] m_split_text;
    string m_input_text, m_output_text;
    List<int> split_number_list;
#endregion

    public override void Awake()
    {
        m_input_text = null;
        m_output_text = null;

        split_number_list = new List<int>();
    }

    /// <summary>
    /// splite number and add in to list
    /// </summary>
    void InitList()
    {
        m_input_text = m_input_txt.GetComponent<InputField>().text;

        // split text of inputfield
        m_split_text = m_input_text.Split(',');

        // add splited text into int list(split_number_list) 
        for (int count = 0; count < m_split_text.Length; count++) {
            split_number_list.Add(int.Parse(m_split_text[count]));
        }
    }

    /// <summary>
    /// Show number list
    /// </summary>
    void ShowText()
    {
        for (int count = 0; count < split_number_list.Count; count++) {
            m_output_text += split_number_list[count].ToString() + " ";
        }

        // Display result of SelectSort
        m_answer_txt.text = m_output_text;
    }
```
![2022-04-29-HeapSort_000](https://user-images.githubusercontent.com/40765022/166093945-b77e9b75-c2dd-4d33-a4a6-97fb30f0821e.png)
<br><br>

[초기화, 정렬, 출력을 실행] <br>
``` C#
    /// <summary>
    /// activate when press enter
    /// </summary>
    public void OnclickEnter()
    {
        InitList();
        SelectSort();
        ShowText();
    }
```
<br>

[선택정렬]<br>
``` C#
    /// <summary>
    /// Select Sort
    /// </summary>
    /// <param name="root_num">first num</param>
    /// <param name="max_num">last num</param>
    private void SelectSort()
    {
        for(int count = 0; count < split_number_list.Count; count++) {
            int _min = count;
            for(int section = count+1; section < split_number_list.Count; section++) {
                if(split_number_list[_min] > split_number_list[section]) {
                    _min = section;
                }
            }
            Swap(count, _min);
            Debug.Log("Process");
            for(int state = 0; state < split_number_list.Count; state ++) {
                Debug.Log(split_number_list[state] + " , ");
            }
        }
    }

    /// <summary>
    /// Swap number which is in splited list
    /// </summary>
    /// <param name="num_1">first num</param>
    /// <param name="num_2">second num</param>
    private void Swap(int num_1, int num_2)
    {
        int temp = split_number_list[num_1];
        split_number_list[num_1] = split_number_list[num_2];
        split_number_list[num_2] = temp;
    }
```
<br>

[전체 코드]<br>
``` C#
public class SelectSortManager : BaseTemplateClass
{
#region private
    [SerializeField] InputField m_input_txt;
    [SerializeField] Text m_answer_txt;

    string[] m_split_text;
    string m_input_text, m_output_text;
    List<int> split_number_list;
#endregion

    public override void Awake()
    {
        m_input_text = null;
        m_output_text = null;

        split_number_list = new List<int>();
    }

    /// <summary>
    /// splite number and add in to list
    /// </summary>
    void InitList()
    {
        m_input_text = m_input_txt.GetComponent<InputField>().text;

        // split text of inputfield
        m_split_text = m_input_text.Split(',');

        // add splited text into int list(split_number_list) 
        for (int count = 0; count < m_split_text.Length; count++) {
            split_number_list.Add(int.Parse(m_split_text[count]));
        }
    }

    /// <summary>
    /// Select Sort
    /// </summary>
    /// <param name="root_num">first num</param>
    /// <param name="max_num">last num</param>
    private void SelectSort()
    {
        for(int count = 0; count < split_number_list.Count; count++) {
            int _min = count;
            for(int section = count+1; section < split_number_list.Count; section++) {
                if(split_number_list[_min] > split_number_list[section]) {
                    _min = section;
                }
            }
            Swap(count, _min);
            Debug.Log("Process");
            for(int state = 0; state < split_number_list.Count; state ++) {
                Debug.Log(split_number_list[state] + " , ");
            }
        }
    }

    /// <summary>
    /// Swap number which is in splited list
    /// </summary>
    /// <param name="num_1">first num</param>
    /// <param name="num_2">second num</param>
    private void Swap(int num_1, int num_2)
    {
        int temp = split_number_list[num_1];
        split_number_list[num_1] = split_number_list[num_2];
        split_number_list[num_2] = temp;
    }

    /// <summary>
    /// Show number list
    /// </summary>
    void ShowText()
    {
        for (int count = 0; count < split_number_list.Count; count++) {
            m_output_text += split_number_list[count].ToString() + " ";
        }

        // Display result of SelectSort
        m_answer_txt.text = m_output_text;
    }

    /// <summary>
    /// activate when press enter
    /// </summary>
    public void OnclickEnter()
    {
        InitList();
        SelectSort();
        ShowText();
    }
}

```
<br>

[Top](#){: .btn .btn--primary }{: .align-right}
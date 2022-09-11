---
title:  "[Algorithm] MergeSort"
excerpt: Unity에서 사용하는 합병 정렬(MergeSort)

categories:
  - Algorithm
tags:
  - [Algorithm, MergeSort, 합병 정렬, 정렬]

toc: true
toc_sticky: true
 
date: 2022-04-30
last_modified_at: 2022-04-30
---

## 개요
#### 합병 정렬(MergeSort)이란?
=> 분할 정복 알고리즘중 하나로 일반적으로 사용되는 정렬방식.<br> 
 구현했을때 안정 정렬에 속한다.<br> 
---

#### 분할 정복 방법 <br> 
* 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
* 대개 순환 호출을 이용하여 구현한다.
---

#### 정렬하는 과정
1. 분할(Devide) : 입력 배열을 같은 크기의 2개으 ㅣ부분 배열로 분할 한다.
2. 정복(Conquer) : 부분배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다.
3. 결합(Combine) : 정렬된 부분 배열들을 하나의 배열에 합병한다.
<br>

![mergesort](https://user-images.githubusercontent.com/40765022/189512910-63127b9d-d415-4308-be86-5b0840ccb2c2.jpg)
> (이미지 출처 :https://medium.com/@paulsoham/merge-sort-63d75df76388)

<br>

* 장점
  * 항상 동일한 시간이 소요되기 때문에 어떤 경우에도 좋은 성능을 보장받을 수 있다.

*  단점
   * 정렬할 데이터의 양이 많은 경우에는 그만큼 이동횟수가 많아지므로 시간적 낭비도 많아지게 된다.
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
    private void InitList()
    {
        m_input_text = m_input_txt.GetComponent<InputField>().text;

        // split text of inputfield
        m_split_text = m_input_text.Split(',');

        // add splited text into int list(split_number_list) 
        for (int count = 0; count < m_split_text.Length; count++)
        {
            split_number_list.Add(int.Parse(m_split_text[count]));
        }
    }

    /// <summary>
    /// Show number list
    /// </summary>
    private void ShowText(List<int> _list_data)
    {
        for (int count = 0; count < _list_data.Count; count++)
        {
            m_output_text += _list_data[count].ToString() + " ";
        }

        // Display result of Sort
        m_answer_txt.text = m_output_text;
    }
```
<br>

[초기와 및 마지소트 실행]<br>

``` C#

    /// <summary>
    /// activate when press enter
    /// </summary>
    private void OnclickEnter()
    {
        InitList();
        ShowText(Devide(split_number_list));
    }
```
<br>

[정렬]<br>
``` C#
    private List<int> Merge(List<int> _left_list, List<int> _right_list)
    {
        //_left_list.Sort((a, b) => { return a > b ? 1 :-1; });
        List<int> mergedList = new List<int>();
        int leftIndex = 0;
        int rightIndex = 0;

        while((leftIndex < _left_list.Count) && (rightIndex < _right_list.Count))
        {
            if (_left_list[leftIndex] <= _right_list[rightIndex]) {
                mergedList.Add(_left_list[leftIndex]);
                leftIndex++;
            } else {
                mergedList.Add(_right_list[rightIndex]);
                rightIndex++;
            }
        }

        if(_left_list.Count > leftIndex) {
            for (int count = leftIndex; count < _left_list.Count; count++) {
                mergedList.Add(_left_list[count]);
            }
        } else if(_right_list.Count > rightIndex) {
            for (int count = rightIndex; count < _right_list.Count; count++) {
                mergedList.Add(_right_list[count]);
            }
        }

        return mergedList;
    }

    private List<int> Devide(List<int> _list)
    {
        if (_list.Count <= 1) return _list;
        int _middle_point = _list.Count / 2;

        List<int> _left_list = _list.ToList();
        List<int> _right_list = _list.ToList();

        _left_list.RemoveRange(_middle_point, (_list.Count - _middle_point));
        _left_list = Devide(_left_list);

        _right_list.RemoveRange(0, _middle_point);
        _right_list = Devide(_right_list);

        return Merge(_left_list, _right_list);
    }
```
<br>

[전체 코드]<br>
``` C#
public class MergeSortManager : BaseTemplateClass
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
    private void InitList()
    {
        m_input_text = m_input_txt.GetComponent<InputField>().text;

        // split text of inputfield
        m_split_text = m_input_text.Split(',');

        // add splited text into int list(split_number_list) 
        for (int count = 0; count < m_split_text.Length; count++)
        {
            split_number_list.Add(int.Parse(m_split_text[count]));
        }
    }

    /// <summary>
    /// Show number list
    /// </summary>
    private void ShowText(List<int> _list_data)
    {
        for (int count = 0; count < _list_data.Count; count++)
        {
            m_output_text += _list_data[count].ToString() + " ";
        }

        // Display result of Sort
        m_answer_txt.text = m_output_text;
    }

    private List<int> Merge(List<int> _left_list, List<int> _right_list)
    {
        //_left_list.Sort((a, b) => { return a > b ? 1 :-1; });
        List<int> mergedList = new List<int>();
        int leftIndex = 0;
        int rightIndex = 0;

        while((leftIndex < _left_list.Count) && (rightIndex < _right_list.Count))
        {
            if (_left_list[leftIndex] <= _right_list[rightIndex]) {
                mergedList.Add(_left_list[leftIndex]);
                leftIndex++;
            } else {
                mergedList.Add(_right_list[rightIndex]);
                rightIndex++;
            }
        }

        if(_left_list.Count > leftIndex) {
            for (int count = leftIndex; count < _left_list.Count; count++) {
                mergedList.Add(_left_list[count]);
            }
        } else if(_right_list.Count > rightIndex) {
            for (int count = rightIndex; count < _right_list.Count; count++) {
                mergedList.Add(_right_list[count]);
            }
        }

        return mergedList;
    }

    private List<int> Devide(List<int> _list)
    {
        if (_list.Count <= 1) return _list;
        int _middle_point = _list.Count / 2;

        List<int> _left_list = _list.ToList();
        List<int> _right_list = _list.ToList();

        _left_list.RemoveRange(_middle_point, (_list.Count - _middle_point));
        _left_list = Devide(_left_list);

        _right_list.RemoveRange(0, _middle_point);
        _right_list = Devide(_right_list);

        return Merge(_left_list, _right_list);
    }

    /// <summary>
    /// activate when press enter
    /// </summary>
    private void OnclickEnter()
    {
        InitList();
        ShowText(Devide(split_number_list));
    }
}
```
<br>


[Top](#){: .btn .btn--primary }{: .align-right}
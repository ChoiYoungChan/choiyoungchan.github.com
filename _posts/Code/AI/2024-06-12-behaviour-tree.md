---
title:  "[AI] 행동 트리를 이용한 AI 개발"
excerpt: AI using Behaviour Tree

categories:
  - AI
tags:
  - [AI, ML 행동 트리행동 트리, Behaviour Tree]

toc: true
toc_sticky: true
 
date: 2024-06-12
last_modified_at: 2024-06-12
---

## Behaviour Tree의 개념
---
```Behavior Tree```는 AI 구현에서 행동을 구조적으로 설계하고 관리하기 위한 계층적 트리 구조입니다. 복잡한 AI 로직을 단순화하고 확장성을 높이는 데 효과적입니다. <br>
Unity에서는 Behavior Tree를 직접 구현하거나, Bolt, NodeCanvas, Behavior Designer 같은 플러그인을 사용할 수 있습니다.<br><br>

![Behaviour_Tree](https://github.com/user-attachments/assets/5a37c4d3-33a2-4422-b77d-7aa97137bf12)<br><br>


### 구성요소
---
1. Root 노드
    * 트리의 시작점으로, 하나의 자식 노드만 가질 수 있습니다.

2. Composite 노드
    * 여러 자식 노드를 관리하며, 조건에 따라 실행 순서를 제어합니다.
      * Selector: 자식 노드 중 하나라도 성공하면 성공.
      * Sequence: 모든 자식 노드가 성공해야 성공.

3. Decorator 노드
    * 자식 노드의 실행을 제어하거나 조건을 추가합니다.<br>
      (ex. 특정 조건이 참일 때만 자식 노드를 실행)

4. Leaf 노드
    * 실제 행동(Behavior)을 수행하는 노드입니다.<br>
      예: 이동, 공격, 대기 등


### 장단점
---
#### 장점
* 유연성: 다양한 AI 로직을 구현할 수 있습니다.
* 가독성: 시각적인 트리 구조로 인해 코드를 쉽게 이해할 수 있습니다.
* 확장성: 새로운 행동이나 조건을 추가하기 쉽습니다.
* 재사용성: 여러 캐릭터에게 동일한 Behavior Tree를 사용할 수 있습니다.

#### 단점
* 복잡한 구현: 직접 구현하는 경우 많은 시간과 노력이 필요할 수 있습니다.
* 성능 오버헤드: 복잡한 트리 구조는 성능에 영향을 줄 수 있습니다.
* 디버깅 어려움: 문제 발생 시 디버깅이 어려울 수 있습니다.


<br><br> 

### 작동 방식
---
트리 순회 방식으로 작동합니다.
Root 노드에서 시작해 자식 노드를 순차적으로 탐색하며 이때 각 노드는 성공(Success), 실패(Failure), 실행 중(Running) 상태를 반환합니다.<br>
이때 노드가 반환한 상태에 따라 다음 행동을 판단하여 수행하는 방식입니다.<br><br>

노드 상태
* Success: 작업이 성공적으로 완료됨.
* Failure: 작업이 실패했거나 조건이 충족되지 않음.
* Running: 작업이 아직 진행 중이며 완료되지 않음.

<br><br>


## 코드
---

[기본 구조 구현]
```c#
using System.Collections.Generic;
using UnityEngine;

public abstract class Node
{
    public enum NodeState { Success, Failure, Running }
    protected NodeState state;

    public NodeState State => state;

    public abstract NodeState Evaluate();
}

```

[Composite 노드 구현]
```c#
public class Selector : Node
{
    private List<Node> children = new List<Node>();

    public Selector(List<Node> children)
    {
        this.children = children;
    }

    public override NodeState Evaluate()
    {
        foreach (var child in children)
        {
            NodeState result = child.Evaluate();
            if (result == NodeState.Success)
            {
                state = NodeState.Success;
                return state;
            }
            else if (result == NodeState.Running)
            {
                state = NodeState.Running;
                return state;
            }
        }
        state = NodeState.Failure;
        return state;
    }
}

public class Sequence : Node
{
    private List<Node> children = new List<Node>();

    public Sequence(List<Node> children)
    {
        this.children = children;
    }

    public override NodeState Evaluate()
    {
        foreach (var child in children)
        {
            NodeState result = child.Evaluate();
            if (result == NodeState.Failure)
            {
                state = NodeState.Failure;
                return state;
            }
            else if (result == NodeState.Running)
            {
                state = NodeState.Running;
                return state;
            }
        }
        state = NodeState.Success;
        return state;
    }
}

```

[Leaf 노드 구현]
```c#
public class MoveToTarget : Node
{
    private Transform transform;
    private Transform target;
    private float speed;

    public MoveToTarget(Transform transform, Transform target, float speed)
    {
        this.transform = transform;
        this.target = target;
        this.speed = speed;
    }

    public override NodeState Evaluate()
    {
        if (Vector3.Distance(transform.position, target.position) > 0.1f)
        {
            transform.position = Vector3.MoveTowards(transform.position, target.position, speed * Time.deltaTime);
            state = NodeState.Running;
        }
        else
        {
            state = NodeState.Success;
        }
        return state;
    }
}

public class CheckTargetInRange : Node
{
    private Transform transform;
    private Transform target;
    private float range;

    public CheckTargetInRange(Transform transform, Transform target, float range)
    {
        this.transform = transform;
        this.target = target;
        this.range = range;
    }

    public override NodeState Evaluate()
    {
        float distance = Vector3.Distance(transform.position, target.position);
        if (distance <= range)
        {
            state = NodeState.Success;
        }
        else
        {
            state = NodeState.Failure;
        }
        return state;
    }
}

```

[Behavior Tree 구성]
```c#
using UnityEngine;

public class AIController : MonoBehaviour
{
    public Transform target;
    public float moveSpeed = 2.0f;
    public float attackRange = 1.5f;

    private Node rootNode;

    private void Start()
    {
        // Leaf 노드
        Node moveToTarget = new MoveToTarget(transform, target, moveSpeed);
        Node checkTargetInRange = new CheckTargetInRange(transform, target, attackRange);

        // Composite 노드
        Sequence attackSequence = new Sequence(new List<Node> { checkTargetInRange, moveToTarget });

        // Root 노드 설정
        rootNode = new Selector(new List<Node> { attackSequence });
    }

    private void Update()
    {
        rootNode.Evaluate();
    }
}

```


<br> 

[Top](#){: .btn .btn--primary }{: .align-right}
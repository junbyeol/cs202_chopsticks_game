# cs202_chopsticks_game

A command-line Chopsticks game built with **F# / .NET 10**.

---

## Getting Started

### Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/download)  
  Verify with: `dotnet --version` (should show `10.x.x`)

### Run

```bash
# Windows
run.bat

# Unix / macOS
chmod +x run.sh
./run.sh

# Or directly
dotnet run
```

### Build

```bash
dotnet build
```

### Publish Self-Contained Binary

```bash
# Windows x64
dotnet publish -c Release -r win-x64 --self-contained

# Linux x64
dotnet publish -c Release -r linux-x64 --self-contained
```

---


## Description
### English

**Project Title**: CLI Chopsticks

**Overview**: This project is a command-line Chopsticks hand game where the user plays against an AI opponent. Each player starts with one finger raised on each hand and takes turns either attacking the
opponent's hand or redistributing their own fingers. A player loses when both of their hands are dead (zero fingers). The user takes the first turn.

**Requirements**:  
1. The user will see the current state of the game in the terminal. At the start of the game, both the user and the AI have 1 finger on each hand (left and right).
2. The user takes the first turn. After that, the user and the AI alternate turns. The user will make a move by responding to prompts in the terminal.
3. On each turn, the active player selects one of two actions: Attack or Split.
  - Attack: The user selects one of their live hands (finger count > 0) and one of the AI's live hands. The finger count of the AI's selected hand increases by the attacker's hand's finger count.
If the result is 5 or greater, the opponent's hand becomes dead (finger count = 0).
      - A dead hand (finger count = 0) cannot be used to attack and cannot be selected as an attack target.
  - Split: The user inputs two integers (left, right). Their sum must equal the user's current total finger count, and each value must be between 0 and 4 inclusive. These become the new finger counts
for the left and right hands.
      - A split whose result is identical to the current configuration is not allowed. Also, a split that merely swaps the left and right values (e.g., (1, 3) → (3, 1)) is not allowed.
    - A split that revives a dead hand (e.g., (0, 4) → (2, 2)) is allowed.
4. If the user enters an invalid action or an invalid selection, the user will be asked to retry the input.
5. The AI selects its action randomly from all valid actions. After each action, the current finger counts of both players are displayed in the terminal.
6. When both of the user's hands are dead, the user loses. When both of the AI's hands are dead, the user wins.

**Example Interaction**: The game prints the current state "User: L[1] R[1] | AI: L[1] R[1]". The user selects Attack, chooses their right hand (1 finger) as the attacking hand, and targets the AI's left hand (1 finger). The result is 1 + 1 = 2, so the AI's left hand now has 2 fingers. The game displays "User: L[1] R[1] | AI: L[2] R[1]" and it is now the AI's turn. The AI takes a random valid action. If the AI attacks the user's right hand with its left hand, the following state is displayed and the turn passes back to the user: "User: L[1] R[3] | AI: L[2] R[1]".


### 한국어
프로젝트 제목: CLI 젓가락 게임

개요: 이 프로젝트는 사용자가 AI 상대와 대결하는 커맨드라인 젓가락 게임입니다. 각 플레이어는 양손에 손가락 하나씩을 펼친 상태로 시작하며, 차례마다 상대의 손을 공격하거나 자신의 손가락을 재배치합니다. 양손이
모두 죽은 손(손가락 0개)이 된 플레이어가 패배합니다. 사용자의 선공으로 시작합니다.

요구사항:
1. 게임 시작 시 플레이어와 AI 모두 왼손과 오른손에 각각 손가락 1개씩을 가진 상태로 시작한다. 터미널에 해당 상태가 표시된다.
2. 플레이어가 먼저 행동하고, 이후 플레이어와 AI가 번갈아 행동한다. 터미널의 질문에 답하며 행동을 정할 수 있다.
3. 각 턴에 행동 중인 플레이어는 때리기와 손뼉치기 중 하나를 선택한다.
   - 때리기: 플레이어는 자신의 살아있는 손(손가락 수 > 0) 중 하나와 상대의 살아있는 손 중 하나를 선택한다. 상대 선택 손의 손가락 수에 공격 손의 손가락 수를 더한다. 결과가 5 이상이면 상대 손은 죽은 손(손가락
수 = 0)이 된다.
     - 죽은 손(손가락 수 = 0)으로는 공격할 수 없으며, 죽은 손을 공격 대상으로 선택할 수 없다.
   - 손뼉치기: 플레이어는 정수 두 개(왼손, 오른손)를 입력한다. 두 값의 합은 현재 플레이어의 총 손가락 수와 같아야 하며, 각 값은 0 이상 4 이하여야 한다. 입력한 값이 새로운 왼손과 오른손의 손가락 수가 된다.
     - 손뼉치기 결과가 현재 상태와 동일한 경우는 허용되지 않는다. 단순히 왼손과 오른손의 값을 맞바꾸는 경우(예: (1, 3) → (3, 1))도 허용되지 않는다.
     - 손뼉치기로 죽은 손을 부활시키는 것(예: (0, 4) → (2, 2))은 허용된다.
4. 플레이어가 유효하지 않은 행동이나 선택을 입력하면 오류 메시지를 표시하고 재입력을 요청한다.
5. AI는 가능한 행동 중에서 무작위로 행동을 선택한다. 각 행동이 끝난 후 계속 터미널에는 현재 손가락 상태가 표시된다.
6. 양손이 모두 죽은 손이 된 플레이어가 패배한다. 게임은 결과(승리 또는 패배)를 표시하고 종료된다.


상호작용 예시: 게임이 시작하면 "User: L[1] R[1] | AI: L[1] R[1]"을 표시한다. 플레이어는 때리기를 선택하고, 자신의 오른손(1개)으로 AI의 왼손(1개)을 공격한다. 결과는 1+1 = 2이므로 AI의 왼손 손가락은 2개가 된다.
게임은 "User: L[1] R[1] | AI: L[2] R[1]"을 표시하고 AI의 턴이 된다. AI는 가능한 행동 중 무작위 행동을 이어한다. 만약, AI가 왼손으로 플레이어의 오른손을 친다면 다음의 상태가 표시되고, 턴은 플레이어에게 넘어간다. "User: L[1] R[3] | AI: L[2] R[1]"

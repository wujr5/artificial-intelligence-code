# 人工智能 Homework2

## 题目

**4.4**
生成大量的八数码问题和八皇后问题并用一下算法分别求解（如果可能的话）：爬山法（最陡上升和首选爬山法），随机重启爬山法，模拟退火算法。计算耗散和问题的解决率，并用图对比它们和最优解代价的曲线。对结果进行评估。

## 大量实例生成算法

```cpp
#include <cstdio>
#include <cstdlib>

#define TESRCASE 100000
#define STEP 10000
#define UP 0
#define DOWN 1
#define LEFT 2
#define RIGHT 3

inline void swap(int *a, int *b) {
    *a ^= *b ^= *a ^= *b;
}

void generate_8_digits_problem() {
    FILE *fp = fopen("testcase_8_digits_problem", "w");
    int testcase = TESRCASE, direction, position, steps;
    while (testcase--) {
        int state[9] = {1, 2, 3, 4, 5, 6, 7, 8, 0};
        steps = STEP;
        position = 9;
        while (steps--) {
            direction = rand() % 4;
            switch (direction) {
                case UP:
                    if (position <= 3)
                        break;
                    else {
                        swap(&state[position - 1], &state[position - 4]), position -= 3;
                        break;
                    }
                case DOWN:
                    if (position >= 7)
                        break;
                    else {
                        swap(&state[position - 1], &state[position + 2]), position += 3;
                        break;
                    }
                case LEFT:
                    if (position % 3 == 1)
                        break;
                    else {
                        swap(&state[position - 1], &state[position - 2]), position--;
                        break;
                    }
                case RIGHT:
                    if (position % 3 == 0)
                        break;
                    else {
                        swap(&state[position - 1], &state[position]), position++;
                        break;
                    }
            }
        }
        fprintf(fp, "%d %d %d %d %d %d %d %d %d\n", state[0], state[1], state[2], state[3], state[4], state[5], state[6], state[7], state[8]);
    }
    fclose(fp);
}

void generate_8_queens_problem() {
    FILE *fp = fopen("testcase_8_queens_problem", "w");
    int testcase = TESRCASE, state[8], position, i;
    while (testcase--) {
        for (i = 0; i < 8; i++)
            position = rand() % 8 + 1, state[i] = position;
        fprintf(fp, "%d %d %d %d %d %d %d %d\n", state[0], state[1], state[2], state[3], state[4], state[5], state[6], state[7]);
    }
    fclose(fp);
}

int main() {
    generate_8_digits_problem();
    generate_8_queens_problem();
    return 0;
}
```

## 爬山法

```cpp
# ifndef CLK_TCK
# define CLK_TCK CLOCKS_PER_SEC
# endif

#include <cstdio>
#include <ctime>
#include <cmath>
#include <cstdlib>
#include <vector>
#include <algorithm>

#define TESRCASE 100000
#define UP 0
#define DOWN 1
#define LEFT 2
#define RIGHT 3

struct State {
    int direction, diff_manhattan;
    State(int i, int dis) {
        this->direction = i;
        this->diff_manhattan = dis;
    }
    bool operator<(const State &s) const {
        return diff_manhattan > s.diff_manhattan;
    }
};

double eight_digits_problem_time;
double eight_queens_problem_time;
int eight_digits_problem_failed_times;
int eight_queens_problem_failed_times;
int diff_manhattan_distance;

inline void swap(int *a, int *b) {
    *a ^= *b ^= *a ^= *b;
}

inline bool solved(int *state) {
    for (int i = 0; i < 8; i++)
        if (state[i] != i + 1)
            return false;
    return true;
}

inline int manhattan_distance(int num, int position) {
    int dest_x = ceil(num / 3), dest_y = (num - 1) % 3 + 1, position_x = ceil(position / 3), position_y = (position - 1) % 3 + 1;
    return abs(dest_x - position_x) + abs(dest_y - position_y);
}

bool eight_digits_better(int *state, int position, int direction) {
    switch (direction) {
        case UP:
            if (position <= 3)
                return false;
            else {
                diff_manhattan_distance =  manhattan_distance(state[position - 4], position - 3) - manhattan_distance(state[position - 4], position);
                return manhattan_distance(state[position - 4], position - 3) > manhattan_distance(state[position - 4], position);
            }
        case DOWN:
            if (position >= 7)
                return false;
            else {
                diff_manhattan_distance = manhattan_distance(state[position + 2], position + 3) - manhattan_distance(state[position + 2], position);
                return manhattan_distance(state[position + 2], position + 3) > manhattan_distance(state[position + 2], position);
            }
        case LEFT:
            if (position % 3 == 1)
                return false;
            else {
                diff_manhattan_distance = manhattan_distance(state[position - 2], position - 1) - manhattan_distance(state[position - 2], position);
                return manhattan_distance(state[position - 2], position - 1) > manhattan_distance(state[position - 2], position);
            }
        case RIGHT:
            if (position % 3 == 0)
                return false;
            else {
                diff_manhattan_distance =  manhattan_distance(state[position], position + 1) - manhattan_distance(state[position], position);
                return manhattan_distance(state[position], position + 1) > manhattan_distance(state[position], position);
            }
    }
    return false;
}

void solve_one_case_of_8_digits_problem(int *state) {
    clock_t start_time = clock();
    int position, i;
    bool found;
    for (i = 0; i < 9; i++)
        if (state[i] == 0) {
            position = i + 1;
            break;
        }
    while (!solved(state)) {
        found = false;
        std::vector<State> v;
        for (i = 0; i < 4; i++) {
            if (eight_digits_better(state, position, i)) {
                found = true;
                v.push_back(State(i, diff_manhattan_distance));
            }
            if (i == 3 && found) {
                std::sort(v.begin(), v.end());
                switch (v[0].direction) {
                    case UP:
                        swap(&state[position - 1], &state[position - 4]), position -= 3;
                        break;
                    case DOWN:
                        swap(&state[position - 1], &state[position + 2]), position += 3;
                        break;
                    case LEFT:
                        swap(&state[position - 1], &state[position - 2]), position--;
                        break;
                    case RIGHT:
                        swap(&state[position - 1], &state[position]), position++;
                        break;
                }
            }
        }
        if (!found) {
            eight_digits_problem_failed_times++;
            return;
        }
    }
    eight_digits_problem_time += (double)(clock() - start_time) / CLK_TCK;
}

void solve_8_digits_problem() {
    FILE *fp = fopen("testcase_8_digits_problem", "r");
    int original_state[9];
    while (fscanf(fp, "%d %d %d %d %d %d %d %d %d", original_state, original_state + 1, original_state + 2, original_state + 3, original_state + 4, original_state + 5, original_state + 6, original_state + 7, original_state + 8) != EOF)
        solve_one_case_of_8_digits_problem(original_state);
    fclose(fp);
}

int peers_of_attacking_queens(int *state) {
    int peers = 0, i, j, k;
    for (i = 0; i < 7; i++) {
        for (j = i + 1; j < 8; j++)
            if (state[j] == state[i])
                peers++;
        for (j = i + 1, k = state[i] + 1; j < 8 && k <= 8; j++, k++)
            if (state[j] == k)
                peers++;
        for (j = i + 1, k = state[i] - 1; j < 8 && k >= 1; j++, k--)
            if (state[j] == k)
                peers++;
    }
    return peers;
}

void solve_one_case_of_8_queens_problem(int *state) {
    clock_t start_time = clock();
    int h = peers_of_attacking_queens(state), i, j, best_i, best_j, temp, record;
    while (h != 0) {
        best_i = -1;
        for (i = 1; i <= 8; i++) {
            record = state[i - 1];
            for (j = 1; j <= 8; j++) {
                if (j != record) {
                    state[i - 1] = j;
                    temp = peers_of_attacking_queens(state);
                    if (temp < h)
                        h = temp, best_i = i, best_j = j;
                }
            }
            state[i - 1] = record;
        }
        if (best_i == -1) {
            eight_queens_problem_failed_times++;
            return;
        }
        state[best_i - 1] = best_j;
    }
    eight_queens_problem_time += (double)(clock() - start_time) / CLK_TCK;
}

void solve_8_queens_problem() {
    FILE *fp = fopen("testcase_8_queens_problem", "r");
    int original_state[8];
    while (fscanf(fp, "%d %d %d %d %d %d %d %d", original_state, original_state + 1, original_state + 2, original_state + 3, original_state + 4, original_state + 5, original_state + 6, original_state + 7) != EOF)
        solve_one_case_of_8_queens_problem(original_state);
    fclose(fp);
}

void print_result() {
    printf("eight digits problem average solved times: %lf\n", eight_digits_problem_time / (double)(TESRCASE - eight_digits_problem_failed_times));
    printf("eight digits problem solved rate: %lf\n", 1 - double(eight_digits_problem_failed_times) / TESRCASE);
    printf("eight queens problem average solved times: %lf\n", eight_queens_problem_time / (double)(TESRCASE - eight_queens_problem_failed_times));
    printf("eight queens problem solved rate: %lf\n", 1 - double(eight_queens_problem_failed_times) / TESRCASE);
}

int main() {
    eight_digits_problem_time = 0;
    eight_queens_problem_time = 0;
    eight_digits_problem_failed_times = 0;
    eight_queens_problem_failed_times = 0;
    solve_8_digits_problem();
    solve_8_queens_problem();
    print_result();
    return 0;
}
```

测试结果：

![](http://images2015.cnblogs.com/blog/687472/201511/687472-20151109095318337-1297820410.jpg)

## 随机重启爬山法

```cpp
# ifndef CLK_TCK
# define CLK_TCK CLOCKS_PER_SEC
# endif

#include <cstdio>
#include <ctime>
#include <cmath>
#include <cstdlib>
#include <vector>
#include <algorithm>

#define TESRCASE 100000
#define STEP 100
#define UP 0
#define DOWN 1
#define LEFT 2
#define RIGHT 3

struct State {
    int direction, diff_manhattan;
    State(int i, int dis) {
        this->direction = i;
        this->diff_manhattan = dis;
    }
    bool operator<(const State &s) const {
        return diff_manhattan > s.diff_manhattan;
    }
};

double eight_digits_problem_time;
double eight_queens_problem_time;
int eight_digits_problem_failed_times;
int eight_queens_problem_failed_times;
int diff_manhattan_distance;

inline void swap(int *a, int *b) {
    *a ^= *b ^= *a ^= *b;
}

inline bool solved(int *state) {
    for (int i = 0; i < 8; i++)
        if (state[i] != i + 1)
            return false;
    return true;
}

inline int manhattan_distance(int num, int position) {
    int dest_x = ceil(num / 3), dest_y = (num - 1) % 3 + 1, position_x = ceil(position / 3), position_y = (position - 1) % 3 + 1;
    return abs(dest_x - position_x) + abs(dest_y - position_y);
}

bool eight_digits_better(int *state, int position, int direction) {
    switch (direction) {
        case UP:
            if (position <= 3)
                return false;
            else {
                diff_manhattan_distance =  manhattan_distance(state[position - 4], position - 3) - manhattan_distance(state[position - 4], position);
                return manhattan_distance(state[position - 4], position - 3) > manhattan_distance(state[position - 4], position);
            }
        case DOWN:
            if (position >= 7)
                return false;
            else {
                diff_manhattan_distance = manhattan_distance(state[position + 2], position + 3) - manhattan_distance(state[position + 2], position);
                return manhattan_distance(state[position + 2], position + 3) > manhattan_distance(state[position + 2], position);
            }
        case LEFT:
            if (position % 3 == 1)
                return false;
            else {
                diff_manhattan_distance = manhattan_distance(state[position - 2], position - 1) - manhattan_distance(state[position - 2], position);
                return manhattan_distance(state[position - 2], position - 1) > manhattan_distance(state[position - 2], position);
            }
        case RIGHT:
            if (position % 3 == 0)
                return false;
            else {
                diff_manhattan_distance =  manhattan_distance(state[position], position + 1) - manhattan_distance(state[position], position);
                return manhattan_distance(state[position], position + 1) > manhattan_distance(state[position], position);
            }
    }
    return false;
}

void eight_digits_random_state(int *s) {
    int state[9] = {1, 2, 3, 4, 5, 6, 7, 8, 0}, steps, position, direction;
    steps = STEP;
    position = 9;
    while (steps--) {
        direction = rand() % 4;
        switch (direction) {
            case UP:
                if (position <= 3)
                    break;
                else {
                    swap(&state[position - 1], &state[position - 4]), position -= 3;
                    break;
                }
            case DOWN:
                if (position >= 7)
                    break;
                else {
                    swap(&state[position - 1], &state[position + 2]), position += 3;
                    break;
                }
            case LEFT:
                if (position % 3 == 1)
                    break;
                else {
                    swap(&state[position - 1], &state[position - 2]), position--;
                    break;
                }
            case RIGHT:
                if (position % 3 == 0)
                    break;
                else {
                    swap(&state[position - 1], &state[position]), position++;
                    break;
                }
        }
    }
    for (int i = 0; i < 9; i++)
        s[i] = state[i];
}

void solve_one_case_of_8_digits_problem(int *state) {
    clock_t start_time = clock();
    int position, i;
    bool found;
    for (i = 0; i < 9; i++)
        if (state[i] == 0) {
            position = i + 1;
            break;
        }
    while (!solved(state)) {
        found = false;
        std::vector<State> v;
        for (i = 0; i < 4; i++) {
            if (eight_digits_better(state, position, i)) {
                found = true;
                v.push_back(State(i, diff_manhattan_distance));
            }
            if (i == 3 && found) {
                std::sort(v.begin(), v.end());
                switch (v[0].direction) {
                    case UP:
                        swap(&state[position - 1], &state[position - 4]), position -= 3;
                        break;
                    case DOWN:
                        swap(&state[position - 1], &state[position + 2]), position += 3;
                        break;
                    case LEFT:
                        swap(&state[position - 1], &state[position - 2]), position--;
                        break;
                    case RIGHT:
                        swap(&state[position - 1], &state[position]), position++;
                        break;
                }
            }
        }
        if (!found)
            eight_digits_random_state(state);
    }
    eight_digits_problem_time += (double)(clock() - start_time) / CLK_TCK;
}

void solve_8_digits_problem() {
    FILE *fp = fopen("testcase_8_digits_problem", "r");
    int original_state[9];
    while (fscanf(fp, "%d %d %d %d %d %d %d %d %d", original_state, original_state + 1, original_state + 2, original_state + 3, original_state + 4, original_state + 5, original_state + 6, original_state + 7, original_state + 8) != EOF)
        solve_one_case_of_8_digits_problem(original_state);
    fclose(fp);
}

int peers_of_attacking_queens(int *state) {
    int peers = 0, i, j, k;
    for (i = 0; i < 7; i++) {
        for (j = i + 1; j < 8; j++)
            if (state[j] == state[i])
                peers++;
        for (j = i + 1, k = state[i] + 1; j < 8 && k <= 8; j++, k++)
            if (state[j] == k)
                peers++;
        for (j = i + 1, k = state[i] - 1; j < 8 && k >= 1; j++, k--)
            if (state[j] == k)
                peers++;
    }
    return peers;
}

inline void eight_queens_random_state(int *state) {
    for (int i = 0; i < 8; i++)
        state[i] = rand() % 8 + 1;
}

void solve_one_case_of_8_queens_problem(int *state) {
    clock_t start_time = clock();
    int h = peers_of_attacking_queens(state), i, j, best_i, best_j, temp, record;
    while (h != 0) {
        best_i = -1;
        for (i = 1; i <= 8; i++) {
            record = state[i - 1];
            for (j = 1; j <= 8; j++) {
                if (j != record) {
                    state[i - 1] = j;
                    temp = peers_of_attacking_queens(state);
                    if (temp < h)
                        h = temp, best_i = i, best_j = j;
                }
            }
            state[i - 1] = record;
        }
        if (best_i == -1)
            eight_queens_random_state(state), h = peers_of_attacking_queens(state);
        else
            state[best_i - 1] = best_j;
    }
    eight_queens_problem_time += (double)(clock() - start_time) / CLK_TCK;
}

void solve_8_queens_problem() {
    FILE *fp = fopen("testcase_8_queens_problem", "r");
    int original_state[8];
    while (fscanf(fp, "%d %d %d %d %d %d %d %d", original_state, original_state + 1, original_state + 2, original_state + 3, original_state + 4, original_state + 5, original_state + 6, original_state + 7) != EOF)
        solve_one_case_of_8_queens_problem(original_state);
    fclose(fp);
}

void print_result() {
    printf("eight digits problem average solved times: %lf\n", eight_digits_problem_time / (double)(TESRCASE - eight_digits_problem_failed_times));
    printf("eight digits problem solved rate: %lf\n", 1 - double(eight_digits_problem_failed_times) / TESRCASE);
    printf("eight queens problem average solved times: %lf\n", eight_queens_problem_time / (double)(TESRCASE - eight_queens_problem_failed_times));
    printf("eight queens problem solved rate: %lf\n", 1 - double(eight_queens_problem_failed_times) / TESRCASE);
}

int main() {
    eight_digits_problem_time = 0;
    eight_queens_problem_time = 0;
    eight_digits_problem_failed_times = 0;
    eight_queens_problem_failed_times = 0;
    solve_8_digits_problem();
    solve_8_queens_problem();
    print_result();
    return 0;
}
```

测试结果：

![](http://images2015.cnblogs.com/blog/687472/201511/687472-20151109100012025-1333982936.jpg)

## 模拟退火算法

```cpp
# ifndef CLK_TCK
# define CLK_TCK CLOCKS_PER_SEC
# endif

#include <cstdio>
#include <ctime>
#include <cmath>
#include <cstdlib>
#include <vector>
#include <algorithm>

#define TESRCASE 100000
#define UP 0
#define DOWN 1
#define LEFT 2
#define RIGHT 3
#define EIGHT_DIGITS_ORIGINAL_TEMPERATURE 10
#define EIGHT_QUEENS_ORIGINAL_TEMPERATURE 50
#define MAX_TRIES_IN_ONE_TEMPERATURE 300
#define STOP_TEMPERATURE 0.000000001
#define COLD_DOWN_RATE 0.8

double eight_digits_problem_time;
double eight_queens_problem_time;
int eight_digits_problem_failed_times;
int eight_queens_problem_failed_times;
double temperature;

inline void swap(int *a, int *b) {
    *a ^= *b ^= *a ^= *b;
}

inline bool solved(int *state) {
    for (int i = 0; i < 8; i++)
        if (state[i] != i + 1)
            return false;
    return true;
}

inline int manhattan_distance(int num, int position) {
    int dest_x = ceil(num / 3), dest_y = (num - 1) % 3 + 1, position_x = ceil(position / 3), position_y = (position - 1) % 3 + 1;
    return abs(dest_x - position_x) + abs(dest_y - position_y);
}

bool eight_digits_better(int *state, int position, int direction) {
    int dis;
    switch (direction) {
        case UP:
            if (position <= 3)
                return false;
            else {
                dis = manhattan_distance(state[position - 4], position - 3) - manhattan_distance(state[position - 4], position);
                return (dis > 0) ? true : ((double)(rand() % 1000) / 1000) < exp(dis / temperature);
            }
        case DOWN:
            if (position >= 7)
                return false;
            else {
                dis = manhattan_distance(state[position + 2], position + 3) - manhattan_distance(state[position + 2], position);
                return (dis > 0) ? true : ((double)(rand() % 1000) / 1000) < exp(dis / temperature);
            }
        case LEFT:
            if (position % 3 == 1)
                return false;
            else {
                dis = manhattan_distance(state[position - 2], position - 1) - manhattan_distance(state[position - 2], position);
                return (dis > 0) ? true : ((double)(rand() % 1000) / 1000) < exp(dis / temperature);
            }
        case RIGHT:
            if (position % 3 == 0)
                return false;
            else {
                dis = manhattan_distance(state[position], position + 1) - manhattan_distance(state[position], position);
                return (dis > 0) ? true : ((double)(rand() % 1000) / 1000) < exp(dis / temperature);
            }
    }
    return false;
}

void solve_one_case_of_8_digits_problem(int *state) {
    clock_t start_time = clock();
    int position, i, tries_count;
    bool found;
    for (i = 0; i < 9; i++)
        if (state[i] == 0) {
            position = i + 1;
            break;
        }
    temperature = EIGHT_DIGITS_ORIGINAL_TEMPERATURE;
    tries_count = MAX_TRIES_IN_ONE_TEMPERATURE;
    while (!solved(state)) {
        found = false;
        for (i = 0; i < 4; i++)
            if (eight_digits_better(state, position, i)) {
                found = true;
                switch (i) {
                    case UP:
                        swap(&state[position - 1], &state[position - 4]), position -= 3;
                        break;
                    case DOWN:
                        swap(&state[position - 1], &state[position + 2]), position += 3;
                        break;
                    case LEFT:
                        swap(&state[position - 1], &state[position - 2]), position--;
                        break;
                    case RIGHT:
                        swap(&state[position - 1], &state[position]), position++;
                        break;
                }
                break;
            }
        if (--tries_count == 0)
            tries_count = MAX_TRIES_IN_ONE_TEMPERATURE, temperature *= COLD_DOWN_RATE;
        if (!found || temperature < STOP_TEMPERATURE) {
            eight_digits_problem_failed_times++;
            return;
        }
    }
    eight_digits_problem_time += (double)(clock() - start_time) / CLK_TCK;
}

void solve_8_digits_problem() {
    FILE *fp = fopen("testcase_8_digits_problem", "r");
    int original_state[9];
    while (fscanf(fp, "%d %d %d %d %d %d %d %d %d", original_state, original_state + 1, original_state + 2, original_state + 3, original_state + 4, original_state + 5, original_state + 6, original_state + 7, original_state + 8) != EOF)
        solve_one_case_of_8_digits_problem(original_state);
    fclose(fp);
}

int peers_of_attacking_queens(int *state) {
    int peers = 0, i, j, k;
    for (i = 0; i < 7; i++) {
        for (j = i + 1; j < 8; j++)
            if (state[j] == state[i])
                peers++;
        for (j = i + 1, k = state[i] + 1; j < 8 && k <= 8; j++, k++)
            if (state[j] == k)
                peers++;
        for (j = i + 1, k = state[i] - 1; j < 8 && k >= 1; j++, k--)
            if (state[j] == k)
                peers++;
    }
    return peers;
}

void solve_one_case_of_8_queens_problem(int *state) {
    clock_t start_time = clock();
    int h = peers_of_attacking_queens(state), i, j, best_i, best_j, temp, record, tries_count, temp_h;
    temperature = EIGHT_QUEENS_ORIGINAL_TEMPERATURE;
    tries_count = MAX_TRIES_IN_ONE_TEMPERATURE;
    while (h != 0) {
        temp_h = 28;
        for (i = 1; i <= 8; i++) {
            record = state[i - 1];
            for (j = 1; j <= 8; j++) {
                if (j != record) {
                    state[i - 1] = j;
                    temp = peers_of_attacking_queens(state);
                    if (temp < temp_h)
                        temp_h = temp, best_i = i, best_j = j;
                }
            }
            state[i - 1] = record;
        }
        if (--tries_count == 0)
            tries_count = MAX_TRIES_IN_ONE_TEMPERATURE, temperature *= COLD_DOWN_RATE;
        if (!(temperature < STOP_TEMPERATURE) && (temp_h < h || ((double)(rand() % 1000) / 1000) < exp(temp_h / temperature)))
            state[best_i - 1] = best_j, h = temp_h;
        else {
            eight_queens_problem_failed_times++;
            return;
        }
    }
    eight_queens_problem_time += (double)(clock() - start_time) / CLK_TCK;
}

void solve_8_queens_problem() {
    FILE *fp = fopen("testcase_8_queens_problem", "r");
    int original_state[8];
    while (fscanf(fp, "%d %d %d %d %d %d %d %d", original_state, original_state + 1, original_state + 2, original_state + 3, original_state + 4, original_state + 5, original_state + 6, original_state + 7) != EOF)
        solve_one_case_of_8_queens_problem(original_state);
    fclose(fp);
}

void print_result() {
    printf("eight digits problem average solved times: %lf\n", eight_digits_problem_time / (double)(TESRCASE - eight_digits_problem_failed_times));
    printf("eight digits problem solved rate: %lf\n", 1 - double(eight_digits_problem_failed_times) / TESRCASE);
    printf("eight queens problem average solved times: %lf\n", eight_queens_problem_time / (double)(TESRCASE - eight_queens_problem_failed_times));
    printf("eight queens problem solved rate: %lf\n", 1 - double(eight_queens_problem_failed_times) / TESRCASE);
}

int main() {
    eight_digits_problem_time = 0;
    eight_queens_problem_time = 0;
    eight_digits_problem_failed_times = 0;
    eight_queens_problem_failed_times = 0;
    solve_8_digits_problem();
    solve_8_queens_problem();
    print_result();
    return 0;
}
```

测试结果：

![](http://images2015.cnblogs.com/blog/687472/201511/687472-20151109101011009-2131768044.jpg)

结论：

总体上模拟退火算法性能更优秀。

**5.16**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey2y69r3ivj21kw16ojzz.jpg)

a.
![](http://ww3.sinaimg.cn/large/ed796d65gw1ezyycuveqyj20vk0h6wga.jpg)

b.跟定点1-6，我们需要寻找7，8：如果7，8都是无穷的，那么，最小节点的值和机会节点都会变得无穷大，最好的移动会发生改变。给定节点1-7，不需要看8。即使8是正无穷的，最小的节点不可能大于-1，所以机会节点不会大于-0.5，所以最好的移动不会改变。

c. 最坏的情况是，如果第三和第四个节点都是-2，那么机会节点就会是0，最好的情况是，他们都是2，这样机会几点是2，所以必须处于0-2之间。

d.如图所示
![](http://ww3.sinaimg.cn/large/ed796d65gw1ezyycuveqyj20vk0h6wga.jpg)

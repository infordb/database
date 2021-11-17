# database


## 트랜잭션
* Atomicyty(원자성) : 트랜잭션 내 명령들을 모두 성공 또는 모두 실패 되어야 한다. 
* Consistency (일관성) : 트랜잭션이 시작될 때 일관성이 있는  상태의 데이터베이스는 트랜잭션에 의해 일관된 상태로 유지돼야 한다.    
명시적인 일관성 :  기본 키, 외래 키   
비명시적인 일관성 : 계좌이체의 경우 두 계좌의 잔고는 이체 전후가 동일해야 한다. 
* Isolation (고립화) : 트랜잭션은 다른 트랜잭션에 영향을 줄/받을 수 없다.  (UNDO)
* Durability (지속성, 영구성): 성공한 트랜잭션에 의한 모든 변경은 영구적으로 유지돼야 한다.   
                              장애가 발생해도 데이터 유실이 없어야 한다. (REDO)



## redo / undo
![image](https://user-images.githubusercontent.com/10610884/142140847-62307cfb-dc12-4d20-ad83-7cada0367050.png)




## Isolation Levels 
* Dirty Read : uncommitted 된 데이터를 읽지 않아야만
* Non Repeatable Read : select 중에 다른 tx 가수정한 commit 된 데이터를 읽지 않음
* Phantom Read : select 중에 다른 tx가 입력한 commit된 데이터를 읽지 않음

## Mariadb Isolation Levels 
1. Read Uncommitted 
2. Read Committed : Dirty Read 만 발생 안함
3. Repeatable Read : Repeatable Read 까지 발생 안함 (마리아DB는 3level까지 적용해도 Phantom Read 발생 안함
4. Serializable : select시 락 발생

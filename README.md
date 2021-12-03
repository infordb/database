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
| 구분  | redo          | undo                        |
|-----|---------------|-----------------------------|
| 역할  | 재생            | 되돌리기                        |
| 용도  | 복구            | rollback, 읽기 일관성, flashback |
| 보호  | 데이터 손실 방지     | 멀티 유저의 읽기 일관성 보호            |
| 저장소 | redo log file | undo segment                |


## Isolation Levels 
* Dirty Read : uncommitted 된 데이터를 읽지 않아야만
* Non Repeatable Read : select 중에 다른 tx 가수정한 commit 된 데이터를 읽지 않음
* Phantom Read : select 중에 다른 tx가 입력한 commit된 데이터를 읽지 않음

## Mariadb Isolation Levels 
1. Read Uncommitted 
2. Read Committed : Dirty Read 만 발생 안함
3. Repeatable Read : Repeatable Read 까지 발생 안함 (마리아DB는 3level까지 적용해도 Phantom Read 발생 안함
4. Serializable : select시 락 발생

oracle = READ COMMITTED  
mysql = REPEATABLE READ

## DB별 고려 사항
 - 선행 트랜잭션이 읽은 데이터는 트랜잭션이 종료될 때까지 후행 트랜잭션이 갱신하거나 삭제하는 것을 불허함으로써 같은 데이터를 두번 쿼리했을 때 일관성 있는 결과를 리턴
 - Phantom Read 현상 발생
 - DB2, SQL Server의 경우 트랜잭션 고립화 수준을 Repeatable Read로 변경하면 읽은 데이터에 걸린 공유 Lock을 커밋할 때까지 유지하는 방식으로 구현
 - Oracle은 이 레벨을 명시적으로 지원하지 않지만 for update절을 이용해 구현 가능,
   SQL Server등에서도 for update 절을 사용할 수 있지만 커서를 명시적으로 선언할 때만 사용 가능함

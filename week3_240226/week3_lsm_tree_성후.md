# LSM Tree

Log Structured Storage Engine

- Log File 기반으로 작동하는 저장소
- append-only 방식으로 저장 → 이미 저장된 데이터는 immutable

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/37b36a73-7840-4632-859d-6e87a432d5bb/Untitled.png)

- Write Performance Good : O(1)
- Read Performance Bad : O(n)

- DB Get을 빠르게 하기 위해 Index 를 생성
- key-value 구조로 데이터의 byte offset 을 인덱스에 저장
- Read Performance 향상

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/a4bd58f8-98d5-4d56-9b05-ca8597a5dadc/Untitled.png)

- 추가적인 Data Structure 가 생기기 때문에 Memory, Disk 소모
- DB write 할 때 Index 도 업데이트 해야한다 → write performance ⬇️

### 문제점

- outdate 된 데이터가 디스크에 누적되는 구조
- append-only 형식으로 디스크 공간 부족 이슈 발생할 수 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/081bba16-b3e5-4704-a3e2-d7d6202ec31c/Untitled.png)

- 낭비되는 용량을 줄이기 위해 Segment File 과 Compaction 개념 도입

### Segmentation

- 하나의 파일로 데이터를 쌓지 않고, 일정 크기가 되면 새로운 파일을 만든다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/83b29b99-6247-4a8b-a0ae-29a2c62899c2/Untitled.png)

### Compaction

- Segment File 을 스캔하면서 중복되는 키 데이터에 compaction 진행
- 더 이상 참조하지 않는 데이터를 삭제
- 저장공간 ⬆️, Segment File 의 용량 줄어듬

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/8f2febae-fc91-4d93-8709-75354411a778/Untitled.png)

- Segment와 Compaction 으로 향상된 Search
- 하지만 hash index에 모든 key가 존재해야함.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/31317d6a-ae44-4104-8bd3-48143526cd35/Untitled.png)

### LSM Tree

- SS(Sorted String) Table 을 사용해서 위에 언급한 단점을 개선
- Segment File 과 비슷하지만 파일 안에 key 로 정렬되어 저장된 구조

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/b94b5421-3ea1-4c25-9213-4eb7d80808f7/Untitled.png)

- 하지만 sort 치려면 append-only가 불가하다.
- 이를 해결하기 위해 memtable 등장

### Memtable

- key-value 가 저장될 때, `Memtable` 이라 불리는 Self-Balancing 이진트리에 데이터를 저장
- key 를 기준으로 정렬된 형태로 저장 가능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/ff51a6dc-0dc1-4859-9c70-bc3b7053418b/Untitled.png)

- memory의 memtable 에 데이터를 추가하다가 일정 사이즈가 넘어가면 트리의 내용을 SS Table 로 저장
- Memtable 은 이미 정렬된 구조이기 때문에 SS Table에 정렬된 순서로 빠르게 Write 가능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/5c205465-0d42-4889-997a-8495a1b92202/Untitled.png)

### LSM Tree - Read

- 이전과 달리 모든 key 가 Index에 존재할 필요 없다.
    - 왜냐하면 SS Table 은 이미 정렬된 상태로 데이터를 저장하기 때문.
    - byte offset 을 이용해 좁은 범위의 데이터를 스캔하여 빠른 조회 가능
    - Range Query 도 가능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/5a00a156-8b62-4347-b75c-cee578c115b1/Untitled.png)

- SS Table 이 점점 많아지는 이슈 존재
- 이제 SS Table 에 대해 Compaction 을 진행 → 사이즈는 크지만 하나의 SS Table 로 (merge) 저장 가능.
- 개별 SS Table 은 sorted 상태기 때문에 merge sort 하기 쉽다 → compaction 비용이 크지 않음

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3a1b7be8-f339-41be-ada3-0da4ec08f87e/9404cf3a-bf7e-4606-869d-bf7ce912f538/Untitled.png)

### LSM Tree 정리

- Write 빠름
- Index 가 Sparse 해도 된다.
- Range query
- LevelDB, RocksDB 등 많은 NoSql 에서 LSM Tree 사용.

Q. sstable 중복 이슈 질문(짐니님) → sstable compaction에도 중복 키 제거할 수 ㅣㅇㅆ다.

Q. LSM Trees는 왜 B Tree 는 사용하지 않았을까?

- 클러스터인덱스, 커버링인덱스
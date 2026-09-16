---
id: LEGACY-MASTER-ROADMAP-V2
type: legacy
status: archived
project: "[[10-project/Project VstState|Project VstState]]"
source_path: ../../Research/ET4920_HighPerformance_State_Management_Master_Roadmap_v2.md
source_version: "2.0"
snapshot_date: 2026-09-16
evidence_level: legacy-unverified
created: 2026-09-16
updated: 2026-09-16
tags:
  - legacy-unverified
---

> [!danger] Immutable legacy snapshot
> Nội dung dưới đây là snapshot lịch sử. Expected results và performance numbers không được dùng như evidence nếu chưa có run/raw data được kiểm chứng.

# MASTER ROADMAP ET4920 v2.0 — VstState / VstUPF-Lab
## High-Performance State Management for Stateful Network Functions — A 5G UPF Case Study
### Từ nền tảng A–Z → tự code lại VstHelper → nghiên cứu hệ thống → prototype → benchmark → luận văn → bảo vệ → portfolio doanh nghiệp

> **Phiên bản:** 2.0 — Research & Industry Edition  
> **Ngày lập:** 16/09/2026  
> **Mục tiêu:** tài liệu “single source of truth” để học lại từ đầu, tự code lại VstHelper/VstState, chia task, kiểm soát claim, thiết kế benchmark, hoàn thiện ET4920 và biến kết quả thành portfolio Systems/Networking/Telecom.  
> **Nguyên tắc:** không coi bất kỳ kết quả hiệu năng cũ nào là “đúng sẵn”. Mọi claim phải được tái hiện bằng code, raw data và benchmark có thể lặp lại.

---

# 0. TL;DR — Ta đang làm gì?

## 0.1. Tên đề tài làm việc

### Tên chính thức đề xuất — Tiếng Việt

**Nghiên cứu và đánh giá kiến trúc quản lý trạng thái hiệu năng cao cho các chức năng mạng có trạng thái, ứng dụng thử nghiệm trong 5G User Plane Function.**

### Tên chính thức đề xuất — Tiếng Anh

**Design and Evaluation of High-Performance State Management for Stateful Network Functions: A 5G UPF Case Study**

### Vì sao tên này được ưu tiên

Tên đề tài **không đặt sẵn kết luận** rằng `Cache-Conscious`, `Zero-GC`, `32-byte layout`, `Hybrid Index` hay bất kỳ kỹ thuật nào chắc chắn tốt hơn. Chúng là **candidate techniques / hypotheses** cần kiểm chứng.

Các tên phụ chỉ dùng sau khi có dữ liệu đủ mạnh:

- `A Cache-Conscious State Engine ...` — chỉ khi hardware counters hỗ trợ claim locality.
- `A Low-Allocation/Zero-Allocation State Engine ...` — chỉ khi hot-path measurement xác nhận.
- `A Hybrid State Engine ...` — chỉ khi Hybrid thực sự là contribution chính.

> **Nguyên tắc đặt tên nghiên cứu:** Problem first, solution second, result last.

## 0.2. Nói đơn giản

Ta nghiên cứu cách lưu và tra cứu **state** của hệ thống mạng sao cho:

- lookup nhanh;
- insert/update/delete đủ nhanh;
- chịu được nhiều thread;
- tail latency ổn định;
- ít tốn RAM;
- ít hoặc không tạo allocation trên hot path;
- giải thích được **vì sao** nhanh/chậm qua CPU/cache/locking/memory behavior.

Sau đó lấy **5G UPF** làm case study:

```text
GTP-U packet
    |
    v
Parse TEID / QFI
    |
    v
State lookup
    |
    +--> PDR/FAR/QER-like rule
    |
    v
FORWARD / DROP / COUNT
```

Không làm cả mạng 5G. Không làm gNodeB. Không làm AMF/SMF hoàn chỉnh. Không cạnh tranh trực tiếp với UPF thương mại.

## 0.3. Sản phẩm cuối cùng

- `VstState` — state engine;
- `VstBench` — benchmark harness;
- `VstTraffic` — traffic/workload generator;
- `VstUPF-Lab` — 5G UPF case-study prototype;
- `VstResults` — scripts/raw data/plots;
- `VstPaper` — báo cáo/paper.

Kiến trúc mục tiêu:

```text
                    +----------------------+
                    |   Control Workload   |
                    | Create/Update/Delete |
                    +----------+-----------+
                               |
                               v
+----------------+     +-------+--------+
| Traffic Gen    | --> | GTP-U Parser   |
+----------------+     +-------+--------+
                               |
                           TEID/QFI
                               |
                               v
                    +--------------------+
                    | IStateBackend      |
                    +--------------------+
                      |      |       |
                      v      v       v
                   .NET    VstState  Hybrid
                   Hash
                      \      |       /
                       +-----+------+
                             |
                             v
                     PDR/FAR-like state
                             |
                  +----------+----------+
                  |                     |
                  v                     v
               FORWARD                DROP
```

---


# 0A. DECISION RECORD — VÌ SAO ĐÂY LÀ ĐỀ TÀI THẬT, KHÔNG PHẢI “BỊA RA”

## 0A.1. Bài toán có tồn tại trong research community

Các công trình công khai cho thấy **state management / stateful packet processing for network functions** là một nhánh nghiên cứu thật:

1. **FlexState: Flexible State Management of Network Functions** — IEEE Access 2021, DOI `10.1109/ACCESS.2021.3061814`. Công trình nghiên cứu cách tách logic network function khỏi data store, vẫn duy trì performance/scalability.
2. **FAJITA: Stateful Packet Processing at 100 Million pps** — Proceedings of the ACM on Networking / CoNEXT 2024, DOI `10.1145/3676861`. Có repository thí nghiệm công khai.
3. **Network Functions With Dynamic State Management on Programmable Switches** — IEEE Transactions on Networking, 2026, DOI `10.1109/TON.2025.3606501`.

=> Vì vậy cụm bài toán **dynamic/high-performance state management for stateful NFs** là một research domain hợp lệ, không phải chỉ là cách gắn từ khóa 5G vào VstHelper.

---

## 0A.2. Bài toán có liên hệ thực tế với Viettel High Tech

Bằng chứng công khai của VHT cho thấy họ quan tâm đúng lớp vấn đề **packet/rule processing, throughput, predictable latency, 5G UPF, DPDK, acceleration**:

- VHT công bố nghiên cứu **“Efficient FPGA Architecture for DPDK Flow Rules Processing”**, nhắm tới xử lý lượng lớn flow rules, có ngữ cảnh áp dụng cho 5G UPF và network functions.
- VHT từng công bố giải pháp **5G UPF Acceleration** cùng hệ sinh thái Intel FPGA/SmartNIC, nhấn mạnh throughput và predictable/reliable latency.
- Các mô tả tuyển dụng công khai của nhóm Network Protocol/5G–6G nhấn mạnh performance, throughput, latency, load, GTP-U/core-network understanding.

**Điều được phép kết luận:** đề tài nằm đúng miền kỹ thuật VHT công khai nghiên cứu/tuyển dụng.

**Điều KHÔNG được kết luận:** VstState tối ưu được UPF proprietary của VHT, hay VstState nhanh hơn sản phẩm VHT/Ericsson/Nokia.

---

## 0A.3. Vì sao không chọn “xây cả UPF”

Một đề tài cử nhân không nên cạnh tranh feature completeness với Open5GS/free5GC/OAI/VHT. Thay vào đó, ta chọn **một vấn đề hẹp nhưng sâu**:

```text
Full 5G Core
   |
   +-- AMF
   +-- SMF
   +-- UPF
        |
        +-- packet parsing
        +-- tunnel handling
        +-- rule/state management   <--- phạm vi nghiên cứu chính
        +-- counters
        +-- forwarding action
```

Đây cũng là cách R&D doanh nghiệp thường tách bài toán: tối ưu một module, một data path, một rule table, một allocator, một scheduling/acceleration mechanism.

---

# 0B. ĐỀ TÀI NÀY CÓ “SẢN PHẨM” KHÔNG?

## 0B.1. Sản phẩm không đồng nghĩa PCB/FPGA

Artifact cuối phải là **một hệ thống chạy được**, không phải “thư viện C# + vài biểu đồ”.

### Sản phẩm bắt buộc

`VstResearch Platform` gồm:

1. `VstState.Core` — state engine;
2. `ManagedBaseline` — baseline cùng runtime;
3. `VstBench` — workload/benchmark harness;
4. `VstTraffic` — traffic generator;
5. `VstUPF-Lab` — GTP-U/UPF-like case study;
6. `VstProfiler` — collector cho runtime + perf data;
7. `VstResults` — raw/processed data + plot scripts;
8. tài liệu build/run/reproduce.

### Demo vật lý khuyến khích nhưng không bắt buộc

```text
[Traffic Generator PC]
          |
       Ethernet
          |
          v
[Device Under Test PC]
    VstUPF-Lab
          |
          v
  Metrics / raw data
```

Nếu chỉ có một máy, dùng loopback/network namespaces trước. Nếu có 2.5/10 GbE sau này, nâng testbed — **không mua hardware chỉ để “trông có phần cứng”**.

---

# 0C. BENCHMARK KHÔNG CẦN SOURCE CỦA VENDOR

## 0C.1. Quy tắc

Không benchmark “VstState vs Viettel UPF” nếu không có cùng workload/config/source/telemetry.

Thay vào đó dùng ba tầng baseline:

### Tầng A — Controlled baseline

- `.NET Dictionary`;
- `.NET ConcurrentDictionary`;
- custom hash nếu cần;
- VstState;
- Hybrid.

Tất cả cùng CPU/runtime/dataset/workload.

### Tầng B — Open industrial baseline

- **DPDK `rte_hash`**: API hiện hành hỗ trợ lookup/bulk lookup và các mode reader-writer concurrency/lock-free reader-writer tùy cấu hình.

### Tầng C — Open telecom reference

- **Open5GS UPF** / `ogs_hash` architecture/source;
- free5GC dùng để hiểu architecture và datapath/control split.

=> Vendor proprietary không phải “chuẩn vàng”. Trong systems research, **reproducible open baseline** thường khoa học hơn một black-box commercial product không kiểm soát được configuration.

---

# 0D. TIÊU CHÍ THÀNH CÔNG CỦA ĐỀ TÀI

Đề tài KHÔNG cần chứng minh “VstState thắng tất cả”.

Thành công nếu trả lời rõ bằng dữ liệu:

1. VstState mạnh/yếu ở workload nào?
2. Chi phí lookup vs mutation là gì?
3. Memory/state ra sao?
4. Tail latency chịu ảnh hưởng bởi allocator/locking/cache như thế nào?
5. Scaling 1→N core bị giới hạn ở đâu?
6. Có cần Hybrid không?
7. Khi đưa vào 5G UPF-like datapath, state access chiếm bao nhiêu end-to-end cost?

Một kết quả kiểu **“Hash thắng point lookup, Vst compact store thắng memory/scan, Hybrid cân bằng tốt hơn”** là một kết quả nghiên cứu hợp lệ và có thể mạnh hơn việc cố chứng minh VstHelper luôn nhanh nhất.

---

# 1. NGUYÊN TẮC NGHIÊN CỨU BẮT BUỘC

## 1.1. Không bắt đầu bằng kết luận

**Sai:** “VstHelper nhanh hơn Hash 3× vì cache-conscious.”  
**Đúng:** “Ta giả thuyết cache-conscious layout có thể cải thiện locality hoặc memory efficiency trong một số workload; ta thiết kế thí nghiệm để kiểm chứng.”

## 1.2. Phân biệt 4 loại phát biểu

| Loại | Ví dụ | Cách xử lý |
|---|---|---|
| Fact | `KeyEntry` được layout 32 B trong implementation | kiểm tra bằng `sizeof`/source |
| Hypothesis | 32 B layout giảm cache miss | benchmark hardware counters |
| Observation | p99 thấp hơn baseline trên máy X | raw data + CI |
| Generalization | kiến trúc phù hợp UPF nói chung | nêu giới hạn, không suy diễn quá mức |

## 1.3. Không lấy số cũ làm ground truth

Các claim cũ như “cache miss giảm 40–50%”, “0 GC tuyệt đối”, “REP MOVSB luôn được sinh”, “memory mapped file = zero-copy”, “AtomicReplace tương đương WAL”, “sorted index chắc chắn hơn hash” đều phải kiểm tra lại.

## 1.4. Reproducibility trước đồ thị đẹp

Mỗi benchmark lưu:

- commit hash;
- OS/kernel;
- runtime/JIT;
- CPU/RAM;
- power mode/governor;
- affinity;
- dataset seed;
- command line;
- raw output;
- timestamp;
- benchmark version.

---

# 2. ET4920 — PHẢI ĐÁP ỨNG GÌ?

## 2.1. Thông tin cần nhớ

Nguồn HUST hiện hành xác nhận `ET4920` là **Đồ án nghiên cứu Cử nhân / Bachelor of Science Research Project**, 8 tín chỉ. Mục tiêu chính thức bao gồm đề xuất giải pháp kỹ thuật và tham gia thiết kế/chế tạo sản phẩm/hệ thống trong Điện tử–Viễn thông.

> **Theo khóa:** tài liệu chương trình cũ và trang mới có thể khác cách ghi phân bố giờ `8(0-0-16-16)` / `8(0-0-16-32)`. Phải xác nhận đúng đề cương áp dụng cho khóa của bạn với SIS/giảng viên.

## 2.2. ET4920 không đồng nghĩa

Không có căn cứ công khai để nói ET4920 bắt buộc:

- FPGA/PCB;
- thiết bị vật lý;
- paper IEEE;
- p99.9;
- `perf`;
- công bố quốc tế.

Với đề tài này, **prototype + benchmark + phân tích định lượng** là cách mạnh để chứng minh hàm lượng nghiên cứu.

## 2.3. Một ET4920 mạnh nên có

### A. Problem statement

Network function cần state access nhanh trong khi state liên tục thêm/xóa/cập nhật. Hash tối ưu exact lookup; compact sorted store có locality tốt nhưng mutation có thể đắt. Cần đánh giá trade-off và thiết kế kiến trúc cân bằng.

### B. Research gap

Không viết “không ai làm”. Viết cụ thể: chưa biết kiến trúc VstHelper-style hoạt động ra sao dưới **dynamic network-state workload** trong môi trường thực nghiệm xác định.

### C. Research Questions

- **RQ1:** Cache-conscious compact layout ảnh hưởng thế nào tới throughput/latency/memory-state so với hash baseline?
- **RQ2:** Dưới `lookup + insert + update + delete`, trade-off là gì?
- **RQ3:** Scalability 1 → 2 → 4 → 8+ thread ra sao?
- **RQ4:** Trong UPF-like prototype, state access chiếm bao nhiêu end-to-end cost?
- **RQ5 (nếu cần):** Hash index + compact state store có cân bằng được lookup/update/memory/tail latency không?

### D. Baselines

Tối thiểu:

1. `Dictionary<TKey,TValue>`;
2. `ConcurrentDictionary<TKey,TValue>`;
3. VstState;
4. VstState-Hybrid nếu có.

Nâng cao:

5. DPDK `rte_hash`;
6. Open5GS `ogs_hash`/UPF state reference;
7. custom native hash nhỏ.

### E. Workloads

- read-only;
- read-heavy;
- mixed;
- churn;
- expiry;
- concurrency scaling.

### F. Metrics

- throughput;
- p50/p95/p99/p99.9;
- memory/state;
- RSS;
- allocated bytes/op;
- GC count/pause;
- CPU% / cycles / instructions;
- cache/branch misses;
- scalability.

### G. Research artifact

- source;
- build script;
- dataset generator;
- benchmark command;
- raw results;
- plot script;
- README;
- report.

---

# 3. PHẠM VI ĐỒ ÁN

## 3.1. Core scope — bắt buộc

1. Rebuild VstHelper core để hiểu bản chất.
2. Tách state-engine API.
3. Viết ít nhất 2 baseline.
4. Thiết kế workload.
5. Benchmark state engine.
6. Viết GTP-U/UPF-like case study.
7. Đo định lượng.
8. Viết báo cáo ET4920.
9. Demo.

## 3.2. Extended scope

- Linux-native memory API;
- XDP/eBPF;
- DPDK baseline;
- Open5GS extracted baseline;
- persistence/recovery;
- AES-GCM state protection;
- NUMA/hugepages;
- multi-machine 10 GbE testbed.

## 3.3. Không thuộc scope ban đầu

- full 5G Core;
- real gNodeB;
- commercial UPF;
- full PFCP;
- full NAT/firewall;
- FPGA SmartNIC;
- distributed consensus;
- full ACID DB;
- GUI lớn.

---

# 4. BẢN ĐỒ KIẾN THỨC

```text
Math / Statistics / Algorithms
          |
          v
Computer Architecture
          |
          +-------------------+
          |                   |
          v                   v
Operating Systems         Data Communication
          |                   |
          v                   v
Concurrency / Memory      Networking
          |                   |
          +---------+---------+
                    |
                    v
              VstState Core
                    |
          +---------+---------+
          |                   |
          v                   v
Benchmarking            Telecom / 5G
          |                   |
          +---------+---------+
                    |
                    v
                VstUPF-Lab
                    |
                    v
             ET4920 Report
```

---

# 5. KIẾN THỨC NỀN PHẢI HỌC LẠI

# 5A. C/C++/C# SYSTEMS PROGRAMMING

## Cần hiểu

- value/reference semantics;
- stack/heap;
- pointers, pointer arithmetic;
- alignment;
- struct layout;
- endianness;
- overflow;
- bit operations;
- virtual dispatch;
- generics;
- unsafe;
- P/Invoke;
- ownership/lifetime;
- use-after-free/double-free/OOB;
- race condition.

## .NET riêng

- CLR;
- managed heap;
- GC generations/LOH;
- pinned memory;
- `Span<T>`/`Memory<T>`;
- `unsafe`, `fixed`, `stackalloc`;
- `Marshal.AllocHGlobal` / `NativeMemory`;
- `Interlocked`/`Volatile`;
- Thread/Task/ThreadPool;
- JIT/tiered compilation.

## Lab

- [ ] `sizeof` struct;
- [ ] dump địa chỉ array;
- [ ] unsafe buffer;
- [ ] memcpy nhỏ;
- [ ] `byte[]` vs stackalloc vs native;
- [ ] race + CAS/lock;
- [ ] BenchmarkDotNet allocation.

## DoD

Giải thích được: pointer ở đâu, ai sở hữu memory, lúc nào free, vì sao race, vì sao allocation gây GC pressure, vì sao “0 allocation” không đồng nghĩa “0 jitter”.

---

# 5B. CẤU TRÚC DỮ LIỆU & GIẢI THUẬT

## Bắt buộc

- array/dynamic array;
- linked list;
- stack/queue/ring buffer;
- heap;
- hash table: chaining/open addressing/cuckoo;
- binary search;
- sorted array;
- BST/RB-tree;
- B/B+tree kiến trúc;
- bloom filter cơ bản.

## Sorting

- insertion;
- quicksort;
- Hoare/Lomuto;
- pivot;
- introsort;
- mergesort;
- parallel sort;
- cache behavior.

## Nhớ

`O(1)` không có nghĩa luôn nhanh hơn `O(log N)` trên mọi N/hardware.

## Lab

- [ ] simple hash table;
- [ ] binary search;
- [ ] sorted insertion;
- [ ] lookup vs insert;
- [ ] random vs sequential access;
- [ ] load factor.

---

# 5C. KIẾN TRÚC MÁY TÍNH

## CPU

- pipeline;
- superscalar;
- out-of-order;
- retirement;
- IPC;
- branch predictor;
- dependency;
- memory-level parallelism.

## Cache

- cache line;
- L1/L2/L3;
- associativity;
- temporal/spatial locality;
- hardware prefetch;
- coherence;
- false sharing.

## Memory

- DRAM;
- bandwidth vs latency;
- NUMA;
- TLB;
- pages/huge pages.

## SIMD

- SSE/AVX2/AVX-512 concept;
- vectorization;
- alignment;
- limits of SIMD.

## Lab

- [ ] sequential vs random scan;
- [ ] stride benchmark;
- [ ] 16/32/64/128-byte struct;
- [ ] false sharing;
- [ ] branch predictable/unpredictable;
- [ ] inspect JIT assembly.

## DoD

Giải thích được vì sao `KeyEntry=32B` **có thể** hữu ích nhưng không suy diễn “2 entry/cache line ⇒ giảm đúng 50% miss”.

---

# 5D. XÁC SUẤT, THỐNG KÊ & THIẾT KẾ THỰC NGHIỆM

## Học

- mean/median;
- variance/stddev;
- percentile;
- histogram/eCDF;
- confidence interval;
- outlier;
- warmup;
- seed;
- sample size;
- noise/bias;
- effect size;
- hypothesis testing cơ bản.

## Latency

- p50/p90/p95/p99/p99.9/max.

## Pitfalls

- JIT warmup;
- turbo/thermal throttling;
- frequency scaling;
- background processes;
- NUMA;
- context switch;
- GC;
- OS/SSD cache;
- branch predictor warmup.

## Nguồn

- Raj Jain — *The Art of Computer Systems Performance Analysis*.
- Brendan Gregg — *Systems Performance*.
- BenchmarkDotNet docs.

---

# 6. ET4291 — HỆ ĐIỀU HÀNH

## 6.1. Trọng tâm theo HUST

- OS structure/kernel-user;
- process/thread;
- scheduling;
- synchronization;
- memory/virtual memory;
- file system;
- I/O;
- thiết kế/mô phỏng module OS.

## 6.2. Nội dung A–Z

### OS fundamentals
kernel, user space, syscall, interrupt, exception, privilege, process, thread.

### Process/thread
address space, PCB, context switch, kernel/user threads, scheduling, affinity.

### Concurrency
race, critical section, mutex, spinlock, semaphore, RW lock, condition variable, atomics, CAS, memory ordering, lock-free/wait-free, ABA concept.

### Scheduling
FCFS/SJF/RR/priority/fairness/throughput-latency/affinity.

### Deadlock
4 conditions, prevention, detection, lock ordering.

### Virtual memory
virtual address, page/page table, TLB, page fault, demand paging, swap, COW, working set.

### Allocator
malloc/free concept, fragmentation, slab, arena, freelist, pool.

### Filesystem
metadata, FD, buffered I/O, page cache, mmap, fsync, durability.

### I/O
blocking/nonblocking/async, interrupts, DMA, nuanced zero-copy, io_uring overview.

### Linux performance
`/proc`, `top/htop`, `taskset`, `numactl`, `perf stat`, `perf record`, flamegraph concept.

## 6.3. Mapping

| ET4291 | Đồ án |
|---|---|
| virtual memory | native state memory |
| synchronization | concurrent state |
| CAS | allocator/free-list |
| mmap | persistence |
| scheduling | scaling |
| page/cache | latency |
| file I/O | checkpoint |
| perf | counters |

## 6.4. Lab

- [ ] process/thread demo;
- [ ] mutex vs spin;
- [ ] CAS counter;
- [ ] producer-consumer;
- [ ] fixed-size pool;
- [ ] mmap/MemoryMappedFile;
- [ ] perf counters;
- [ ] affinity.

---

# 7. ET4230 — MẠNG MÁY TÍNH

## Nội dung A–Z

### Layering
OSI, TCP/IP, encapsulation, MTU.

### Ethernet
MAC, frame, switch, VLAN basic, ARP.

### IP
IPv4 header, IPv6 basics, CIDR/subnet, fragmentation, ICMP, TTL.

### Routing
LPM, routing table, static/dynamic, OSPF/BGP concept.

### UDP
Datagram, checksum, no retransmission, socket buffers.

### TCP
handshake, seq/ACK, flow control, congestion, RTT/RTO, retransmission, slow start, HOL.

### NAT/stateful function
conntrack, 5-tuple, state table, expiry.

### Socket
bind/listen/accept/send/recv, UDP, epoll concept, buffer sizing.

### Packet capture
Wireshark/tcpdump/PCAP.

### Linux stack
NIC, driver, RX/TX queues, NAPI concept, kernel stack, userspace.

### High performance
RSS, RPS/RFS, batching, XDP, AF_XDP, DPDK overview.

## Mapping

packet parser, UDP/GTP-U traffic, throughput, packet loss, stateful lookup, traffic benchmark.

## Lab

- [ ] UDP echo;
- [ ] TCP echo;
- [ ] packet parser;
- [ ] Wireshark Ethernet/IP/UDP;
- [ ] traffic generator;
- [ ] PPS/Gbps;
- [ ] packet loss under load.

---

# 8. ET4070 — CƠ SỞ TRUYỀN SỐ LIỆU

## Trọng tâm

HUST hiện mô tả học phần với xác suất, tiến trình ngẫu nhiên, hàng đợi, routing/flow/congestion và mô phỏng/đo hiệu năng.

## Nội dung

### Probability
random variable, Bernoulli, Binomial, Poisson, exponential, expectation, variance.

### Stochastic process
arrival, inter-arrival, memoryless, Poisson process.

### Queueing
`λ`, `μ`, `ρ`, Little's Law, Kendall, M/M/1, M/M/c concept, delay, stability.

### Traffic
burst, offered load, capacity, saturation, drop.

### Performance
throughput, goodput, latency, jitter, loss, queue length.

### Flow/congestion
queue buildup, bufferbloat, backpressure.

### Simulation
discrete-event, synthetic workload, reproducibility.

## Mapping

arrival-rate design, stress, saturation point, queues, latency under load, workload distributions.

## Lab

- [ ] M/M/1 simulation;
- [ ] delay vs utilization;
- [ ] Poisson/burst traffic;
- [ ] state engine under arrival rates;
- [ ] find saturation point.

---

# 9. ET4250 — HỆ THỐNG VIỄN THÔNG

## 9.1. Trọng tâm theo HUST

- hệ thống viễn thông;
- mobile/optical/satellite/microwave;
- modulation/coding/multiple access;
- performance evaluation.

Đồ án ưu tiên **mobile/5G architecture**, không đi sâu RF nếu không phục vụ RQ.

## 9.2. Nền

source/channel/destination, bandwidth, SNR, modulation/coding overview, multiplexing, multiple access, cellular, handover, QoS.

## 9.3. Cellular evolution

2G/3G overview, LTE/EPC, 5G NR vs 5G Core, NSA vs SA concept.

## 9.4. 5G Core bắt buộc

### Network functions
AMF, SMF, UPF, UDM, AUSF, PCF, NRF, NSSF overview.

### Control vs user plane

```text
UE --- RAN --- UPF --- Data Network
       |
       +---- control functions
```

### Interfaces
N3, N4, N6, N9.

### GTP-U
UDP/2152, TEID, tunnel, encapsulation, extension-header/QFI overview.

### PFCP
CUPS, PFCP session, PDR, FAR, QER, URR, BAR overview.

### UPF state
forwarding rules, PFCP rule state, counters, QoS state, tunnel IDs, lifecycle.

## 9.5. Prototype mapping

Không full PFCP. Simplified:

```text
PdrState
- PdrId
- Teid
- Qfi
- Precedence
- FarId

FarState
- FarId
- Action
- Destination
- OuterTeid
```

Packet: `TEID -> lookup -> rule -> action`.

## 9.6. Chuẩn

- 3GPP TS 23.501;
- 3GPP TS 23.502;
- 3GPP TS 29.244;
- Open5GS;
- free5GC tham khảo phụ.

---

# 10. ET3310 — LÝ THUYẾT MẬT MÃ

> Không phải core của RQ chính; dùng làm security extension nếu cần.

## Toán
modular arithmetic, gcd, extended Euclid, primes, finite-field concept, Euler/Fermat.

## Symmetric
block cipher, AES, modes, ECB pitfalls, CTR, GCM, nonce, key management.

## Hash
preimage/second-preimage/collision, SHA-2/SHA-3, cryptographic vs xxHash.

**xxHash không phải security hash. MD5 không dùng cho security mới.**

## MAC/AEAD
HMAC, integrity/authentication, AES-GCM, ChaCha20-Poly1305.

## Public key
RSA/ECC/DH/ECDH/signature concepts.

## Protocol
TLS 1.3, replay, nonce reuse, threat model.

## Extension
- authenticated checkpoint;
- AES-GCM snapshot;
- security overhead benchmark.

---

# 11. HỌC LẠI VSTHELPER TỪ ĐẦU

> Quy trình: **spec → minimal implementation → test → benchmark → đọc source cũ → compare**.

## VST-0 — Spec & contract

- [ ] mục tiêu engine;
- [ ] ownership;
- [ ] errors;
- [ ] lifetime;
- [ ] thread-safety;
- [ ] Windows/Linux portability.

Deliverable: `docs/vst-core-spec.md`.

## VST-1 — Buffer/native memory

- pointer/alignment/allocation/copy/ownership;
- implement `NativeBuffer`, `BufferView`;
- tests + leak checks.

## VST-2 — Fixed slab

V1 lock-based 1 size class → V2 CAS bitmap → V3 multi-size-class.

Benchmark rent/return, threads, contention, overhead.

> Không gọi toàn allocator “lock-free” chỉ vì có CAS ở một đoạn.

## VST-3 — Raw/contiguous list

capacity, grow, insert/remove, ownership; compare `List<T>`.

## VST-4 — Key representation

Không bắt buộc 32B. Thử 16/24/32/64B nếu cần. Test equality/order/hash/collision handling.

## VST-5 — Hashing

Built-in vs xxHash64 vs optional composite fingerprint. Hiểu collision; không nói “collision impossible”.

## VST-6 — Sorted index

binary search, insertion, batch sort, tombstone; benchmark lookup/insert/rebuild.

## VST-7 — Dynamic delta index

```text
      Lookup
        |
 +------+------+
 |             |
 v             v
Delta Hash   Main Sorted
 |             |
 +------+------+
        |
      Result
```

Tasks: mutable delta, compact main, merge policy, tombstones, read/update paths.

## VST-8 — Hybrid hash + compact store

```text
Hash: key -> state index
              |
              v
       Compact state array
```

Study lookup/memory/update/locality.

## VST-9 — Concurrency

global RW lock, sharding, per-bucket, immutable snapshot/delta, CAS where justified. Stress/invariant tests.

## VST-10 — Persistence

buffered write, mmap, fsync, checkpoint, crash consistency, WAL concept.

> `AtomicReplace` không tự động bằng WAL đầy đủ.

## VST-11 — Linux port

- [ ] core không phụ thuộc kernel32;
- [ ] OS abstraction;
- [ ] Windows/Linux CI;
- [ ] Linux perf.

---

# 12. STATE ENGINE API

```csharp
public interface IStateStore<TKey, TValue>
{
    bool TryGet(in TKey key, out TValue value);
    bool TryAdd(in TKey key, in TValue value);
    bool TryUpdate(in TKey key, in TValue value);
    bool TryRemove(in TKey key);
}
```

Mở rộng: bulk lookup, batch update, expiry, scan, stats.

Backends:

```text
ManagedDictionaryStore
ConcurrentDictionaryStore
VstSortedStore
VstHybridStore
OptionalNativeHashStore
```

---

# 13. DATA MODEL

## Generic flow

```text
FlowKey
- src IP
- dst IP
- src port
- dst port
- protocol

FlowState
- firstSeen
- lastSeen
- packets
- bytes
- flags
```

## UPF-like

```text
UpfKey
- TEID
- QFI/direction/discriminator

UpfState
- PDR ID
- FAR ID
- action
- destination
- outer TEID
- counters
- lastSeen
```

---

# 14. BENCHMARK METHODOLOGY

## 14.1. Baseline levels

### Level 1 — controlled .NET

`Dictionary`, `ConcurrentDictionary`, VstState.

### Level 2 — native industry reference

DPDK `rte_hash`.

### Level 3 — telecom reference

Open5GS `ogs_hash`/UPF source. Không tuyên bố “thắng Open5GS toàn hệ thống”.

## 14.2. Workload suite

Lấy tư duy YCSB, tùy biến cho network state.

### NS-A — Read-only
`100% lookup`

### NS-B — Data-plane heavy
`95% lookup / 5% update`

### NS-C — Churn
`90% lookup / 5% insert / 5% delete`

### NS-D — Mixed
`70% lookup / 10% insert / 10% update / 10% delete`

### NS-E — Expiry
1M active state + expire/cleanup.

### NS-F — Burst
sudden state-creation burst.

## 14.3. Dataset

10K / 100K / 1M bắt buộc; 5M/10M nếu RAM đủ.

## 14.4. Threads

1 / 2 / 4 / 8 / physical-core-count.

## 14.5. Key distributions

uniform, sequential, Zipf/skew, hot set, temporal/latest.

## 14.6. Metrics

### Primary
ops/s, p50/p95/p99/p99.9, bytes/state, RSS, scalability.

### Explanatory
cycles, instructions, IPC, cache refs/misses, branches/misses, context switches, page faults, allocation, GC, lock contention.

## 14.7. Protocol

Before: close background apps, power fixed, Release build, fixed seed, affinity if applicable.  
During: warmup + repetitions + raw data.  
After: percentiles/CI/plots/anomaly log.

## 14.8. Không làm

- Debug vs Release;
- different datasets;
- one-run benchmark;
- cherry-pick;
- generated fake numbers;
- unlabeled code changes.

---

# 15. TOOLS

## Core
Git, GitHub/GitLab, .NET 8/10, C#, Linux. WSL dùng học; benchmark cuối ưu tiên Linux thật nếu có.

## Benchmark
BenchmarkDotNet, custom latency recorder, histogram library nếu chọn, `perf`.

## Network
Wireshark, tcpdump, iperf3, tc/netem, Scapy/Python prototype, custom traffic generator.

## Profiling
`perf stat`, `perf record`, FlameGraph, dotnet-counters, dotnet-trace.

## Automation
Bash, Python, CSV/JSON raw, Matplotlib/R.

---

# 16. 5G UPF CASE STUDY — TASK

## 16.1. 5G architecture

- [ ] UE/gNB/Core/DN;
- [ ] AMF/SMF/UPF;
- [ ] control vs user;
- [ ] N3/N4/N6;
- [ ] PDU session.

DoD: tự vẽ và giải thích packet path.

## 16.2. GTP-U

- [ ] header;
- [ ] TEID;
- [ ] UDP;
- [ ] encapsulation;
- [ ] QFI extension overview;
- [ ] parse PCAP;
- [ ] generate synthetic packet.

## 16.3. PFCP/rules

- [ ] PDR/FAR/QER/URR relations;
- [ ] không full PFCP ban đầu.

## 16.4. Minimal datapath

```text
Receive -> validate -> parse -> key -> lookup -> action -> counter
```

## 16.5. Rule lifecycle

create/update/delete/expire.

## 16.6. End-to-end benchmark

Same parser/traffic/machine/rules, **chỉ đổi state backend**.

---

# 17. PHẦN CỨNG — CÓ CẦN KHÔNG?

Không bắt buộc. Có thể dựng testbed:

```text
Traffic PC --- Ethernet --- DUT PC (VstUPF-Lab)
```

Mức 1 loopback → mức 2 hai máy 1GbE → mức 3 2.5/10GbE → mức 4 XDP/DPDK/SmartNIC nếu dư thời gian.

Không mua hardware chỉ để “trông có sản phẩm”.

---

# 18. EXPERIMENT MATRIX

```text
Backends:
- Dictionary
- ConcurrentDictionary
- VstState
- Hybrid

Datasets:
- 10K
- 100K
- 1M

Workloads:
- NS-A...NS-E

Threads:
- 1
- 2
- 4
- 8
```

`4 × 3 × 5 × 4 = 240` experiment cells trước repetitions. Chạy theo phase, không brute-force ngay.

---

# 19. PHASED EXPERIMENT DESIGN

- **E1 correctness** — chưa đo performance.
- **E2 microbenchmark** — per-operation cost.
- **E3 mixed state** — dynamic workload.
- **E4 hardware counters** — giải thích.
- **E5 network integration** — end-to-end.
- **E6 native/open-source baseline** — DPDK/Open5GS.

---

# 20. TIÊU CHÍ SO SÁNH

| Claim | Metric |
|---|---|
| High performance | ops/s, PPS, Gbps |
| Low latency | p50/p95/p99/p99.9 |
| Predictable | variance/tail/jitter |
| Cache-conscious | cache refs/misses, cycles, IPC |
| Low-GC | allocation/op, GC/pause |
| Memory efficient | bytes/state, RSS |
| Concurrent | 1/2/4/8 threads |
| Dynamic | insert/update/delete rates |
| Scalable | N=10K→1M+ |

Không có “con số bí mật của Viettel” làm chuẩn. Chuẩn là **controlled, reproducible comparison**.

---

# 21. SOURCE ĐÓNG CỦA VENDOR

Không cần source Viettel/Ericsson/Nokia. Không claim “VstState nhanh hơn Viettel UPF”.

Dùng:

- open-source baseline;
- standards;
- controlled workloads;
- reproducible metrics;
- peer-reviewed related work.

---

# 22. SECURITY / ET3310 EXTENSION

Sau core:

- S1 HMAC checkpoint;
- S2 AES-GCM persistence;
- S3 secure erase/key-handling study.

Đo overhead throughput/latency/CPU/size.

---

# 23. REPO ĐỀ XUẤT

```text
VstResearch/
+-- docs/
|   +-- proposal/
|   +-- architecture/
|   +-- notes/
|   +-- experiments/
|   +-- reading/
+-- src/
|   +-- Vst.Core/
|   +-- Vst.State/
|   +-- Vst.State.ManagedBaseline/
|   +-- Vst.UpfLab/
|   +-- Vst.Traffic/
+-- benchmarks/
+-- tests/
+-- experiments/
|   +-- configs/
|   +-- scripts/
|   +-- raw/
|   +-- processed/
+-- analysis/
+-- paper/
+-- README.md
```

---

# 24. GIT & RESEARCH HYGIENE

`main` stable, feature branches, experiment tags. Commit mô tả kỹ thuật, không “fix code”.

Ví dụ tag: `exp-v0.3.1-lookup-1m-8t`.

---

# 25. RESEARCH LOG TEMPLATE

```markdown
## Date
### Question
### Hypothesis
### Change
### Experiment
### Result
### Interpretation
### Next step
```

---

# 26. THESIS STRUCTURE

1. Introduction
2. Background
3. Related Work
4. VstState Design
5. 5G UPF Case Study
6. Methodology
7. Results
8. Discussion
9. Conclusion

Phải có **Threats to Validity**.

---

# 27. THREATS TO VALIDITY

## Internal
JIT, noise, allocator warmup, scheduling.

## Construct
synthetic workload đại diện thực tế đến đâu?

## External
one CPU, one OS/runtime, no commercial UPF.

## Conclusion
sample size/statistical uncertainty.

---

# 28. DEMO BẢO VỆ

1. load 1M state và đổi backend;
2. GTP-U-like traffic → TEID → rule/action;
3. perf counters;
4. chủ động demo một trường hợp VstState thua Hash và giải thích/hybrid hóa.

---

# 29. CÂU HỎI HỘI ĐỒNG CÓ THỂ HỎI

- Tại sao không hash table?
- Vì sao 32B?
- Có thực sự giảm cache miss?
- Zero-GC nghĩa gì?
- Memory leak?
- Lock-free chứng minh thế nào?
- Vì sao C# không C/C++?
- DPDK compare có công bằng?
- Workload đại diện thực tế?
- Vì sao 5G UPF?
- TEID/PDR/FAR là gì?
- Tại sao không commercial UPF?
- p99 vì sao?
- 1M state lấy căn cứ đâu?
- Hash thắng thì contribution là gì?
- Linux portability?
- claim nào của bạn, claim nào prior work?

---

# 30. ROADMAP 10 THÁNG

## Tháng 1 — Foundation reset

Architecture, OS, unsafe C#, algorithms, stats. Build mini allocator/hash/sorted array.  
**Gate M1:** tự implement/explain memory + lookup basics.

## Tháng 2 — Rebuild Vst Core

Native memory, slab, raw list, key/hash, tests.  
**M2:** correctness/stress.

## Tháng 3 — Index & Dynamic State

Sorted index, hash baseline, delta/hybrid, state API.  
**M3:** all operations correct.

## Tháng 4 — Concurrency + Linux

locks/sharding/CAS where justified, Linux port, CI.  
**M4:** 1/2/4/8-thread correctness.

## Tháng 5 — Benchmark Suite

workloads/datasets/histograms/raw storage.  
**M5:** reproducible command.

## Tháng 6 — 5G + UPF Lab

23.501, 29.244, GTP-U, TEID, PDR/FAR, traffic generator.  
**M6:** packet→state→action.

## Tháng 7 — Core Experiments

.NET baselines, 10K/100K/1M, A–E workloads, scaling.  
**M7:** raw dataset trả lời RQ1–RQ3.

## Tháng 8 — Profiling / Advanced Baseline

perf/cache/branch, DPDK, optional Open5GS extract.  
**M8:** explanation cho major differences.

## Tháng 9 — Thesis/Paper

figures, discussion, limitations, advisor iterations.  
**M9:** full draft.

## Tháng 10 — Reproducibility + Defense

clean repo, scripted demo, slides, Q&A, rerun, archive.  
**M10:** clone→build→run core benchmark.

---

# 31. WEEKLY TASK TEMPLATE

```markdown
## Wxx — Title
### Objective
### Knowledge
- [ ]
### Implementation
- [ ]
### Experiment
- [ ]
### Reading
- [ ]
### Deliverable
- [ ]
### Definition of Done
- [ ]
### Risks
- [ ]
```

---

# 32. PRIORITY

- **P0:** correctness, state API, baselines, benchmark, report.
- **P1:** Linux, perf, GTP-U, hybrid.
- **P2:** DPDK, Open5GS extracted benchmark, two-PC.
- **P3:** XDP, crypto, NUMA, SmartNIC.

Không làm P2/P3 khi P0 chưa xong.

---

# 33. DEFINITION OF DONE TOÀN ĐỒ ÁN

- [ ] RQ rõ;
- [ ] build sạch;
- [ ] tests pass;
- [ ] ≥3 backends;
- [ ] ≥3 dataset sizes;
- [ ] ≥4 workload profiles;
- [ ] ≥4 thread levels;
- [ ] raw results lưu;
- [ ] benchmark reproducible;
- [ ] 5G case study chạy;
- [ ] không số bịa;
- [ ] claim có data/source;
- [ ] limitations rõ;
- [ ] report hoàn chỉnh;
- [ ] scripted demo;
- [ ] repository clean.

---

# 34. NGUỒN HỌC ƯU TIÊN

## 34.1. HUST

1. SEEE HUST — Kỹ thuật Điện tử - Viễn thông  
   https://seee.hust.edu.vn/vi/dao-tao/et1/

2. ET4291 — Hệ điều hành  
   https://seee.hust.edu.vn/vi/dao-tao/hoc-phan/et4291/

3. ET4230Q — Mạng máy tính  
   https://seee.hust.edu.vn/vi/dao-tao/hoc-phan/et4230q/

4. ET4070Q — Cơ sở truyền số liệu  
   https://seee.hust.edu.vn/en/dao-tao/hoc-phan/et4070q/

5. ET4250 — Hệ thống viễn thông  
   https://seee.hust.edu.vn/vi/dao-tao/hoc-phan/et4250/

> Với khóa cũ ET3310 + mô-đun 5 học phần, dùng đề cương đúng khóa; chương trình hiện hành đã tái cấu trúc.

## 34.2. OS/Systems

- OSTEP — Arpaci-Dusseau.
- CS:APP — Bryant & O'Hallaron.
- Brendan Gregg — *Systems Performance*.
- Linux man pages / `perf`.

## 34.3. Networking

- Kurose & Ross — *Computer Networking: A Top-Down Approach*.
- Tanenbaum — *Computer Networks*.
- RFCs IP/UDP/TCP.
- Wireshark docs.

## 34.4. Data communication/performance

- Raj Jain — *The Art of Computer Systems Performance Analysis*.
- Gross & Harris — *Fundamentals of Queueing Theory*.
- Bertsekas & Gallager — *Data Networks*.

## 34.5. 5G

- 3GPP TS 23.501  
  https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3144
- 3GPP TS 29.244  
  https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3111
- Open5GS  
  https://github.com/open5gs/open5gs
- Open5GS UPF context  
  https://github.com/open5gs/open5gs/blob/main/src/upf/context.c
- free5GC  
  https://free5gc.org/

## 34.6. DPDK

- Hash API: https://doc.dpdk.org/api/rte__hash_8h.html
- Main: https://www.dpdk.org/

## 34.7. Benchmark

- BenchmarkDotNet: https://benchmarkdotnet.org/
- Diagnosers: https://benchmarkdotnet.org/articles/configs/diagnosers.html
- YCSB core workloads: https://github.com/brianfrankcooper/YCSB/blob/master/doc/coreworkloads.html
- YCSB workload method: https://github.com/brianfrankcooper/YCSB/blob/master/doc/workload.html
- perf stat: https://man7.org/linux/man-pages/man1/perf-stat.1.html

## 34.8. Cryptography

- Katz & Lindell — *Introduction to Modern Cryptography*.
- Ferguson/Schneier/Kohno — *Cryptography Engineering*.
- RFC 8446 — TLS 1.3.
- NIST FIPS 197 — AES.
- NIST FIPS 202 — SHA-3.

---

# 35. VSTHELPER CŨ — DÙNG NHƯ THẾ NÀO

Theo tài liệu NCKH hiện có, VstHelper có các khối/ý tưởng:

- unmanaged memory;
- slab allocator;
- `KeyEntry`;
- `KeyIndexer`;
- xxHash;
- raw list;
- serialization helpers;
- Win32 file/mmap;
- lock engine;
- background clock.

Không copy kết luận cũ. Chỉ dùng như:

1. design candidate;
2. source of hypotheses;
3. historical implementation ideas.

Khi có source thật:

```text
for each module:
    read spec
    read source
    write invariants
    rewrite minimal version
    test
    benchmark
    compare old/new
```

---

# 36. CLAIM AUDIT CHECKLIST

Trước khi đưa câu vào báo cáo:

- [ ] Fact hay hypothesis?
- [ ] Có source?
- [ ] Có raw data?
- [ ] Có baseline?
- [ ] Cùng điều kiện?
- [ ] Có repeat?
- [ ] Có limitations?
- [ ] Tái hiện được?

Không thì không viết như kết luận chắc chắn.

---

# 37. KHI SOURCE VSTHELPER ĐƯỢC ĐƯA SAU

1. inventory modules/dependencies/unsafe/OS-specific/API;
2. viết invariants;
3. test hiện trạng trước refactor;
4. benchmark hiện trạng (`VstHelper-old`);
5. rewrite module-by-module;
6. compare correctness/readability/performance/portability.

---

# 38. CHECKPOINT VỚI GIẢNG VIÊN

## Meeting 1
1-page proposal + RQs + scope + architecture + baselines.

Hỏi:
- phạm vi có rộng?
- rubric riêng?
- report format?
- có yêu cầu phần cứng?
- có server/lab/NIC?

## Meeting 2
core engine + early baseline.

## Meeting 3
workload methodology.

## Meeting 4
5G case study.

## Meeting 5+
raw results, không chỉ slides.

---

# 39. PROPOSAL 1 TRANG — SƯỜN

- Title
- Problem
- Motivation
- RQs
- Method
- Baselines
- Metrics
- Prototype
- Expected contributions (không hứa số)
- Risks

---

# 40. EXPECTED CONTRIBUTIONS — CÁCH VIẾT

Không: “VstState nhanh hơn DPDK 2×” khi chưa đo.

Nên:

1. workload suite cho dynamic network state;
2. cache-conscious state-engine implementation;
3. trade-off analysis vs hash baselines;
4. hybrid architecture nếu data ủng hộ;
5. 5G UPF case-study prototype;
6. reproducible scripts/dataset/results.

---

# 41. MỤC TIÊU NGHỀ NGHIỆP

Kỹ năng hình thành:

- systems programming;
- Linux;
- OS/concurrency;
- network protocol;
- performance engineering;
- 5G Core fundamentals;
- benchmarking;
- technical research.

Hướng nghề: Telecom R&D, 5G Core, network systems, cloud networking, NFV/security, storage/database engine, infrastructure, embedded/system software.

Phù hợp để nói chuyện chuyên môn với nhóm network/system R&D như Viettel High Tech, nhưng không được nói prototype này là technology của VHT hoặc benchmark proprietary VHT UPF.

---

# 42. SAU 10 THÁNG PHẢI TỰ TRẢ LỜI ĐƯỢC

### Memory
byte được cấp phát ở đâu? ownership? fragmentation?

### CPU
cache miss, branch miss, IPC?

### Concurrency
race, CAS, memory ordering?

### Network
packet NIC→process thế nào? UDP/GTP-U?

### 5G
UPF, TEID, PDR, FAR?

### Benchmark
p99, warmup, baseline, cross-language limitation?

### Research
hypothesis, evidence, scope/limitations?

Nếu chưa trả lời được thì chưa coi là hiểu source.

---

# 43. NEXT ACTIONS — LÀM NGAY

## Task 001 — Setup repo
- [ ] repo/README/docs/log/references.

## Task 002 — Xác nhận ET4920 theo khóa
- [ ] đề cương/rubric/format/deadline/yêu cầu riêng.

## Task 003 — Foundation diagnostic
- [ ] pointer/cache/hash/binary search/process-thread/TCP-UDP/p99/5G overview.

## Task 004 — Rebuild NativeBuffer
Không đọc source cũ trước.

## Task 005 — Rebuild Fixed Slab
Lock-based trước, CAS sau.

## Task 006 — Baseline Hash
Simple implementation + .NET compare.

## Task 007 — Sorted Index
Binary lookup + mutation benchmark.

## Task 008 — Proposal v0
Sau một số microbenchmark ban đầu.

---

# 44. QUY TẮC CUỐI

1. Correctness > performance.
2. Measurement > intuition.
3. Raw data > screenshot.
4. Baseline > self-comparison.
5. Trade-off > “vô địch”.
6. Small reproducible prototype > huge unfinished system.
7. Hiểu từng layer > copy source cũ.
8. Không bịa số.
9. Không gán claim cho 3GPP/VHT nếu source không nói.
10. Đồ án phải trả lời RQ, không chỉ hoàn thành feature list.

---

# 45. MASTER FLOW

```text
FOUNDATION
  |
  +-- Algorithms
  +-- Architecture
  +-- Statistics
  |
  v
ET4291 + ET4230 + ET4070
  |
  v
Rebuild Vst Core
  |
  +-- memory
  +-- index
  +-- hash
  +-- concurrency
  |
  v
Dynamic VstState
  |
  +-- managed baselines
  +-- workloads
  +-- benchmark
  |
  v
ET4250 / 5G
  |
  v
VstUPF-Lab
  |
  +-- GTP-U
  +-- TEID
  +-- PDR/FAR-like state
  |
  v
Deep Evaluation
  |
  +-- p99
  +-- memory
  +-- cache
  +-- scaling
  |
  v
Discussion / Hybrid Design
  |
  v
ET4920 Thesis + Demo + Defense
```

---

# 46. CẬP NHẬT TÀI LIỆU SAU NÀY

Khi có source VstHelper:
- Codebase Audit;
- file→concept mapping;
- dependency graph;
- rewrite tasks;
- tests;
- benchmark per module.

Khi có rubric/giảng viên:
- ET4920 compliance matrix.

Khi có máy benchmark:
- hardware profile;
- CPU topology;
- protocol.

Khi có early results:
- refine RQs;
- decide Hybrid.

---

# PHỤ LỤC A — ET4920 COMPLIANCE MATRIX

| Hạng mục | Artifact |
|---|---|
| Vấn đề kỹ thuật | Network-state management |
| Giải pháp | VstState architecture |
| Thiết kế | memory/index/concurrency |
| Sản phẩm | VstUPF-Lab |
| Thực nghiệm | benchmark suite |
| Phân tích | performance + counters |
| Kiến thức chuyên ngành | OS + network + data comm + telecom |
| Báo cáo | thesis |
| Bảo vệ | demo + slides + Q&A |

---

# PHỤ LỤC B — LEARNING CHECKLIST

## OS
- [ ] process/thread
- [ ] scheduling
- [ ] synchronization
- [ ] atomics
- [ ] virtual memory
- [ ] allocator
- [ ] mmap
- [ ] filesystem
- [ ] I/O
- [ ] perf

## Network
- [ ] Ethernet/ARP/IP
- [ ] UDP/TCP
- [ ] routing/NAT
- [ ] sockets
- [ ] capture
- [ ] PPS/Gbps

## Data Comm
- [ ] probability/Poisson
- [ ] queueing/Little's Law
- [ ] utilization/latency/loss
- [ ] simulation

## 5G
- [ ] 5GS
- [ ] AMF/SMF/UPF
- [ ] N3/N4/N6
- [ ] GTP-U/TEID
- [ ] PFCP
- [ ] PDR/FAR/QER

## Crypto
- [ ] AES/hash/HMAC/AEAD
- [ ] RSA/ECC concept
- [ ] TLS/threat model

## Research
- [ ] RQ/hypothesis
- [ ] baseline/workload
- [ ] metrics/statistics
- [ ] reproducibility
- [ ] limitations/threats

---

# PHỤ LỤC C — SOURCE PRIORITY

Khi có mâu thuẫn:

1. chuẩn chính thức (3GPP/RFC/NIST);
2. tài liệu HUST chính thức;
3. source code chính thức;
4. official project docs;
5. peer-reviewed paper;
6. textbook;
7. blog kỹ thuật;
8. forum/Reddit;
9. AI answer.

AI dùng để giải thích/brainstorm/review/test ideas — **không phải source of truth** cho claim kỹ thuật.

---


# 47. EXECUTIVE CHECKLIST — 20 CÂU PHẢI “YES” TRƯỚC KHI BẢO VỆ

1. [ ] Tôi mô tả problem mà không nhắc VstHelper trước.
2. [ ] Tôi phân biệt hypothesis và result.
3. [ ] Tôi giải thích vì sao baseline là công bằng.
4. [ ] Tôi có raw data.
5. [ ] Tôi có scripts để reproduce.
6. [ ] Tôi không dùng số benchmark bịa/từ AI.
7. [ ] Tôi biết workload có limitation gì.
8. [ ] Tôi có ít nhất một result “không như kỳ vọng” và giải thích nó.
9. [ ] Tôi đo tail latency, không chỉ average.
10. [ ] Tôi đo memory/state.
11. [ ] Tôi biết bottleneck concurrency nằm đâu.
12. [ ] Tôi hiểu packet path của prototype.
13. [ ] Tôi giải thích TEID/PDR/FAR được.
14. [ ] Tôi không tuyên bố benchmark proprietary vendor.
15. [ ] Tôi biết DPDK/Open5GS được dùng làm reference thế nào.
16. [ ] Tôi hiểu code core do mình tự viết lại.
17. [ ] Tôi có tests correctness/stress.
18. [ ] Tôi nêu threats to validity.
19. [ ] Tôi có demo script không phụ thuộc Internet.
20. [ ] Nếu hội đồng hỏi “VstState thua Hash thì sao?”, tôi có câu trả lời nghiên cứu rõ ràng.

---

# 48. ONE-PARAGRAPH PITCH — PHIÊN BẢN CUỐI

> Đồ án nghiên cứu bài toán quản lý trạng thái động cho các network function hiệu năng cao. Từ nền NCKH VstHelper, em tự xây lại và đánh giá một state engine với các lựa chọn memory layout, allocator, indexing và concurrency khác nhau; so sánh có kiểm soát với hash-based baselines và, ở mức nâng cao, các reference mã nguồn mở như DPDK/Open5GS. Em dùng workload gồm lookup, insert, update, delete, expiry và multi-thread scaling, đo throughput, p99/p99.9, memory/state và hardware/runtime counters để giải thích nguyên nhân. Cuối cùng em tích hợp engine vào một 5G UPF-like prototype xử lý GTP-U/TEID/PDR/FAR ở phạm vi tối giản để kiểm chứng end-to-end. Mục tiêu không phải chứng minh VstState luôn nhanh nhất mà xác định trade-off và, nếu dữ liệu ủng hộ, đề xuất kiến trúc Hybrid phù hợp hơn.

---

**END — Master Roadmap v2.0 — Research & Industry Edition**


 Dear sir,when I train googlenet model,the following message shows.Please help me how to solve.. 

[libprotobuf ERROR google/protobuf/text_format.cc:274] Error parsing text-format caffe.NetParameter: 32:15: Expected string.

F1228 10:23:03.046366  3457 upgrade_proto.cpp:928] Check failed: ReadProtoFromTextFile(param_file, param) Failed to parse NetParameter file: /home/habib/dgd_person_reid/external/caffe/models/bvlc_googlenet/train_val.prototxt

*** Check failure stack trace: ***
    @     0x7f3191e595cd  google::LogMessage::Fail()
    @     0x7f3191e5b433  google::LogMessage::SendToLog()
    @     0x7f3191e5915b  google::LogMessage::Flush()
    @     0x7f3191e5be1e  google::LogMessageFatal::~LogMessageFatal()
    @     0x7f3192579b71  caffe::ReadNetParamsFromTextFileOrDie()
    @     0x7f31925423bf  caffe::Solver<>::InitTrainNet()
    @     0x7f319254359e  caffe::Solver<>::Init()
    @     0x7f3192543766  caffe::Solver<>::Solver()
    @           0x4122e3  caffe::GetSolver<>()
    @           0x4099cd  train()
    @           0x407010  main
    @     0x7f3190b11830  __libc_start_main
    @           0x407629  _start
    @              (nil)  (unknown)
Aborted (core dumped)

#include <rocksdb/db.h>
#include <rocksdb/sst_file_manager.h>
#include <iostream>

int main() {
    rocksdb::Options options;
    rocksdb::DB* db;
    rocksdb::Status status = rocksdb::DB::Open(options, "/path/to/db", &db);
    if (!status.ok()) {
        std::cerr << "Failed to open database: " << status.ToString() << std::endl;
        return 1;
    }

    // Get approximate memtable stats
    rocksdb::TablePropertiesCollection props;
    db->GetApproximateMemTableStats(&props);
    std::cout << "Approximate memtable stats:" << std::endl;
    for (const auto& prop : props) {
        std::cout << "Level: " << prop.first << std::endl;
        std::cout << "  Table count: " << prop.second->num_entries << std::endl;
        std::cout << "  Size: " << prop.second->num_data_bytes << std::endl;
    }

    // Get approximate sizes of SST files in a specific level
    int level = 0;  // The level you want to check
    uint64_t total_size = 0;
    db->GetApproximateSizes(rocksdb::Range(), 1, &level, &total_size);
    std::cout << "Approximate size of SST files in level " << level << ": " << total_size << std::endl;

    delete db;
    return 0;
}

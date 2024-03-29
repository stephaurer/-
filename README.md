# -
智慧城市利用区块链技术和边缘计算,实现城市数据的安全共享和实时处理,优化城市资源配置,提升城市管理效率和居民生活质量。
import hashlib
import time

class Block:
    def __init__(self, index, transactions, timestamp, previous_hash):
        self.index = index
        self.transactions = transactions
        self.timestamp = timestamp
        self.previous_hash = previous_hash
        self.hash = self.compute_hash()

    def compute_hash(self):
        block_string = "{}{}{}{}".format(self.index, self.transactions, self.timestamp, self.previous_hash)
        return hashlib.sha256(block_string.encode()).hexdigest()

class Blockchain:
    def __init__(self):
        self.chain = []
        self.create_genesis_block()

    def create_genesis_block(self):
        genesis_block = Block(0, [], time.time(), "0")
        genesis_block.hash = genesis_block.compute_hash()
        self.chain.append(genesis_block)

    def add_block(self, transactions):
        last_block = self.chain[-1]
        new_block = Block(index=last_block.index + 1,
                          transactions=transactions,
                          timestamp=time.time(),
                          previous_hash=last_block.hash)
        new_block.hash = new_block.compute_hash()
        self.chain.append(new_block)

    def is_chain_valid(self):
        for i in range(1, len(self.chain)):
            current = self.chain[i]
            previous = self.chain[i-1]
            if current.hash != current.compute_hash() or current.previous_hash != previous.hash:
                return False
        return True

# Example usage
blockchain = Blockchain()
blockchain.add_block("City data transaction 1")
blockchain.add_block("City data transaction 2")
print("Blockchain valid?", blockchain.is_chain_valid())
def edge_compute(data):
    # Simulate processing data at the edge
    processed_data = data + " - Processed at the edge"
    return processed_data

# Simulating data processing at the edge
raw_data = "Sensor data from City infrastructure"
processed_data = edge_compute(raw_data)
print(processed_data)

# allocation
class ResourceAllocator:
    def __init__(self, total_resources):
        self.total_resources = total_resources
        self.allocated_resources = {}

    def allocate(self, task, amount):
        if amount > self.total_resources:
            print(f"Not enough resources to allocate {amount} to {task}.")
        else:
            self.allocated_resources[task] = amount
            self.total_resources -= amount
            print(f"Allocated {amount} resources to {task}.")

    def deallocate(self, task):
        if task in self.allocated_resources:
            amount = self.allocated_resources.pop(task)
            self.total_resources += amount
            print(f"Deallocated {amount} resources from {task}.")
        else:
            print(f"No resources allocated to {task}.")

    def status(self):
        print(f"Total resources available: {self.total_resources}")
        print("Current allocations:")
        for task, amount in self.allocated_resources.items():
            print(f"  {task}: {amount} resources")

# Example usage
if __name__ == "__main__":
    allocator = ResourceAllocator(total_resources=100)

    allocator.allocate("Task A", 30)
    allocator.allocate("Task B", 50)
    allocator.allocate("Task C", 25)  # This should fail due to insufficient resources

    allocator.status()

    allocator.deallocate("Task A")
    allocator.allocate("Task C", 25)  # This should succeed now

    allocator.status()

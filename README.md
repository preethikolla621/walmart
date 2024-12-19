class PowerOfTwoMaxHeap {
    constructor(x) {
      this.heap = [];
      this.x = x;
    }
  
  insert(value) {
      this.heap.push(value); // Add the value to the end of the array.
      this._siftUp(this.heap.length - 1); 
    }

   popMax() {
      if (this.heap.length === 0) {
        return undefined; // Return undefined if the heap is empty.
      }
  
  const max = this.heap[0]; // Store the maximum value.
      this.heap[0] = this.heap[this.heap.length - 1]; 
      this.heap.pop(); // Remove the last element from the array.
      this._siftDown(0); // Sift down the root element to its correct position.
  
  return max; 
    }
  
  _siftUp(index) {
      const parent = Math.floor((index - 1) / this.x); // Calculate the parent index using the power of two property.
  
  while (index > 0 && this.heap[index] > this.heap[parent]) {
        [this.heap[index], this.heap[parent]] = [this.heap[parent], this.heap[index]];
        index = parent;
        parent = Math.floor((index - 1) / this.x); // Update the parent index.
      }
    }
    _siftDown(index) {
      let maxChildIndex = this._getMaxChild(index); // Get the index of the maximum child.
      while (maxChildIndex !== -1 && this.heap[index] < this.heap[maxChildIndex]) {
        [this.heap[index], this.heap[maxChildIndex]] = [this.heap[maxChildIndex], this.heap[index]];
        index = maxChildIndex;
        maxChildIndex = this._getMaxChild(index); // Update the maximum child index.
      }
    }
    _getMaxChild(index) {
      const startChild = this.x * index + 1; // Calculate the start index of the children.
      const endChild = Math.min(startChild + this.x, this.heap.length); // Calculate the end index of the children.
      let maxChildIndex = -1;
      let maxChildValue = -Infinity;
      for (let i = startChild; i < endChild; i++) {
        if (this.heap[i] > maxChildValue) {
          maxChildIndex = i;
          maxChildValue = this.heap[i];
        }
      }
  
  return maxChildIndex;
    }
  }  

# Bellman-Ford Algorithm Implementation in Python

Djikstra's: not guaranteed to work when there are negative edges
Bellman-Ford: will not give the correct answer if there is a negative cycle but works with negative edges
Any negative cycle: the answer is always -infinity as you can just go through the negative cycle infinitely for an infinitely short distance

So before solving any shortest path problem, you can check all edges for negative values, and run a dfs for cycle detection and check if the cycle edges sum up to a negative value to figure out what case you're in

## Pseudocode

The Bellman-Ford algorithm finds the shortest paths from a source vertex to all other vertices in a weighted graph, even with negative edge weights.

```
function BellmanFord(graph, source):
    // Initialize distances
    distance[source] = 0
    for all other vertices v:
        distance[v] = infinity

    // Relax edges repeatedly
    for i from 1 to |V|-1:  // |V| is the number of vertices
        for each edge (u, v) with weight w:
            if distance[u] + w < distance[v]:
                distance[v] = distance[u] + w

    // Check for negative weight cycles
    for each edge (u, v) with weight w:
        if distance[u] + w < distance[v]:
            return "Graph contains a negative weight cycle"

    return distance
```

## Basic Implementation

```python
def bellman_ford(graph, source):
    # Step 1: Initialize distances from source to all other vertices as INFINITY
    distances = {vertex: float('infinity') for vertex in graph}
    distances[source] = 0

    # Step 2: Relax all edges |V| - 1 times
    for _ in range(len(graph) - 1):
        for u in graph:
            for v, weight in graph[u].items():
                if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                    distances[v] = distances[u] + weight

    # Step 3: Check for negative-weight cycles
    for u in graph:
        for v, weight in graph[u].items():
            if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                print("Graph contains negative weight cycle")
                return None

    return distances

# Example usage
graph = {
    'A': {'B': -1, 'C': 4},
    'B': {'C': 3, 'D': 2, 'E': 2},
    'C': {},
    'D': {'B': 1, 'C': 5},
    'E': {'D': -3}
}

print(bellman_ford(graph, 'A'))
```

## Variations and Use Cases

### 1. Path Reconstruction Variation

This variation not only finds the shortest distances but also tracks the predecessor of each vertex.

```python
def bellman_ford_with_path(graph, source):
    # Initialize distances and predecessors
    distances = {vertex: float('infinity') for vertex in graph}
    predecessors = {vertex: None for vertex in graph}
    distances[source] = 0

    # Relax edges
    for _ in range(len(graph) - 1):
        for u in graph:
            for v, weight in graph[u].items():
                if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                    distances[v] = distances[u] + weight
                    predecessors[v] = u

    # Check for negative cycles
    for u in graph:
        for v, weight in graph[u].items():
            if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                print("Graph contains negative weight cycle")
                return None, None

    return distances, predecessors

def reconstruct_path(predecessors, target):
    path = []
    current = target
    while current is not None:
        path.append(current)
        current = predecessors[current]
    return path[::-1]  # Reverse to get path from source to target

# Example usage
distances, predecessors = bellman_ford_with_path(graph, 'A')
if distances:
    print(f"Path to E: {reconstruct_path(predecessors, 'E')}")
```

### 2. Early Termination Optimization

This variation stops when no relaxation occurs in an iteration, indicating we've found the shortest paths.

```python
def optimized_bellman_ford(graph, source):
    distances = {vertex: float('infinity') for vertex in graph}
    distances[source] = 0

    for _ in range(len(graph) - 1):
        no_changes = True
        for u in graph:
            for v, weight in graph[u].items():
                if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                    distances[v] = distances[u] + weight
                    no_changes = False

        # If no relaxation occurred in this iteration, we can terminate early
        if no_changes:
            break

    # Check for negative cycles
    for u in graph:
        for v, weight in graph[u].items():
            if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                print("Graph contains negative weight cycle")
                return None

    return distances
```

### 3. SPFA (Shortest Path Faster Algorithm)

A queue-based optimization of Bellman-Ford that often performs better in practice.

```python
from collections import deque

def spfa(graph, source):
    distances = {vertex: float('infinity') for vertex in graph}
    distances[source] = 0

    # Track vertices in queue
    in_queue = {vertex: False for vertex in graph}
    queue = deque([source])
    in_queue[source] = True

    # Track number of times a vertex is processed
    count = {vertex: 0 for vertex in graph}

    while queue:
        u = queue.popleft()
        in_queue[u] = False

        for v, weight in graph[u].items():
            if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                distances[v] = distances[u] + weight

                # If v is not in queue, add it
                if not in_queue[v]:
                    queue.append(v)
                    in_queue[v] = True
                    count[v] += 1

                    # If v has been processed more than |V| times, negative cycle exists
                    if count[v] >= len(graph):
                        print("Graph contains a negative weight cycle")
                        return None

    return distances
```

## Use Cases

1. **Network Routing**: Finding the shortest paths in a network where edge weights represent costs, distances, or times.

2. **Currency Exchange**: Detecting arbitrage opportunities in currency exchange networks (negative cycle detection).

3. **Traffic Flow Analysis**: Modeling traffic networks where edge weights represent travel times.

4. **Maximum Flow Problems**: As a component in solving more complex network flow problems.

5. **Circuit Design**: Finding critical paths in circuit designs with timing constraints.

The key advantages of Bellman-Ford over Dijkstra's algorithm:

- Handles negative edge weights
- Detects negative cycles
- Simpler implementation for dense graphs

The main disadvantage is its time complexity of O(|V|·|E|), which is worse than Dijkstra's algorithm for graphs without negative edges.

# Bellman-Ford Algorithm in Financial Applications

The Bellman-Ford algorithm is particularly valuable in financial contexts due to its ability to handle negative weights and detect negative cycles. Here are practical examples of using this algorithm with financial data:

## 1. Currency Arbitrage Detection

Currency arbitrage is a trading strategy that exploits price differences between different forex markets. The Bellman-Ford algorithm can detect profitable arbitrage opportunities by finding negative cycles in a currency exchange graph.

```python
import math

def detect_arbitrage(exchange_rates):
    """
    Detect arbitrage opportunities in currency exchange rates

    Args:
        exchange_rates: Dictionary mapping currency pairs to exchange rates
                       e.g., {'USD-EUR': 0.85, 'EUR-GBP': 0.9, 'GBP-USD': 1.3}

    Returns:
        List representing an arbitrage cycle, if one exists
    """
    # Extract unique currencies
    currencies = set()
    for pair in exchange_rates:
        currencies.update(pair.split('-'))
    currencies = list(currencies)

    # Build graph: convert exchange rates to negative log values
    # This transforms the multiplication problem into an addition problem
    # and lets us use Bellman-Ford to find negative cycles
    graph = {currency: {} for currency in currencies}
    for pair, rate in exchange_rates.items():
        base, quote = pair.split('-')
        # Use negative log to find arbitrage opportunities
        graph[base][quote] = -math.log(rate)

    # Run Bellman-Ford from an arbitrary source
    source = currencies[0]
    distances = {currency: float('infinity') for currency in currencies}
    predecessors = {currency: None for currency in currencies}
    distances[source] = 0

    # Relax edges |V| - 1 times
    for _ in range(len(currencies) - 1):
        for base in currencies:
            for quote, weight in graph.get(base, {}).items():
                if distances[base] + weight < distances[quote]:
                    distances[quote] = distances[base] + weight
                    predecessors[quote] = base

    # Check for negative cycles
    for base in currencies:
        for quote, weight in graph.get(base, {}).items():
            if distances[base] + weight < distances[quote]:
                # Negative cycle exists, extract it
                cycle = []
                current = base
                visited = set()

                while current not in visited:
                    visited.add(current)
                    cycle.append(current)
                    current = predecessors[current]

                # Complete the cycle
                cycle.append(current)
                # Get the cycle in correct order
                start_idx = cycle.index(current)
                cycle = cycle[start_idx:] + cycle[:start_idx]

                return cycle

    return None

# Example usage
exchange_rates = {
    'USD-EUR': 0.85,
    'EUR-GBP': 0.9,
    'GBP-JPY': 155.0,
    'JPY-USD': 0.0092,
    'USD-JPY': 110.0,
    'EUR-USD': 1.18,
    'GBP-USD': 1.3
}

arbitrage_path = detect_arbitrage(exchange_rates)
if arbitrage_path:
    print(f"Arbitrage opportunity found: {' -> '.join(arbitrage_path)}")

    # Calculate profit from the cycle
    profit = 1.0
    for i in range(len(arbitrage_path) - 1):
        base = arbitrage_path[i]
        quote = arbitrage_path[i+1]
        rate_key = f"{base}-{quote}"
        if rate_key in exchange_rates:
            profit *= exchange_rates[rate_key]
        else:
            # If direct rate not available, use inverse
            inverse_key = f"{quote}-{base}"
            profit *= (1.0 / exchange_rates[inverse_key])

    print(f"Starting with 1 {arbitrage_path[0]}, you end with {profit} {arbitrage_path[0]}")
    print(f"Profit percentage: {(profit - 1) * 100:.2f}%")
else:
    print("No arbitrage opportunity found")
```

This yields negative profit ...

## 2. Portfolio Optimization with Transaction Costs

Here's an example of using Bellman-Ford to find the most cost-efficient way to rebalance a portfolio when considering transaction costs:

```python
def optimal_portfolio_rebalancing(current_allocations, target_allocations, transaction_costs):
    """
    Find the optimal sequence of trades to reach target allocations
    while minimizing transaction costs

    Args:
        current_allocations: Dictionary of current asset allocations
        target_allocations: Dictionary of target asset allocations
        transaction_costs: Dictionary of costs for each possible transaction

    Returns:
        Optimal sequence of trades and total cost
    """
    # Build graph where:
    # - Vertices are possible allocation states
    # - Edges are transactions with costs as weights

    assets = list(current_allocations.keys())

    # Create a simplified graph for this example
    # In a real system, you'd generate all valid allocation states
    graph = {}

    # Start with the current allocation
    start_state = tuple(current_allocations[asset] for asset in assets)
    # Target allocation
    end_state = tuple(target_allocations[asset] for asset in assets)

    # Run Bellman-Ford to find shortest path from current to target allocation
    distances = {start_state: 0}
    predecessors = {start_state: None}

    # In a real implementation, you'd generate the states and transitions dynamically
    # For this example, we'll assume we have these states and transitions:
    states = [start_state]  # In reality, this would be many intermediate states
    states.append(end_state)

    # Add some example intermediate states (in a real system this would be comprehensive)
    # These would be valid portfolio allocations between current and target
    for i in range(5):  # Just a few sample states
        intermediate = []
        for j in range(len(assets)):
            weight = (current_allocations[assets[j]] * (5-i) + target_allocations[assets[j]] * i) / 5
            intermediate.append(round(weight, 2))
        states.append(tuple(intermediate))

    # Generate transaction costs between states
    for from_state in states:
        graph[from_state] = {}
        for to_state in states:
            if from_state != to_state:
                # Calculate transaction cost (simplified for example)
                cost = sum(abs(to_state[i] - from_state[i]) * transaction_costs.get(assets[i], 0.01)
                          for i in range(len(assets)))
                graph[from_state][to_state] = cost

    # Run Bellman-Ford
    for _ in range(len(states) - 1):
        for u in states:
            if u in graph and u in distances:
                for v, weight in graph[u].items():
                    if u != v and (v not in distances or distances[u] + weight < distances[v]):
                        distances[v] = distances[u] + weight
                        predecessors[v] = u

    # Reconstruct optimal path
    if end_state not in distances:
        return None, float('infinity')

    path = []
    current = end_state
    while current is not None:
        path.append(current)
        current = predecessors.get(current)

    path.reverse()
    total_cost = distances[end_state]

    # Convert tuples back to readable asset allocations
    readable_path = []
    for allocation in path:
        allocation_dict = {assets[i]: allocation[i] for i in range(len(assets))}
        readable_path.append(allocation_dict)

    return readable_path, total_cost

# Example usage
current_portfolio = {"Stocks": 0.60, "Bonds": 0.30, "Cash": 0.10}
target_portfolio = {"Stocks": 0.40, "Bonds": 0.50, "Cash": 0.10}
transaction_costs = {"Stocks": 0.02, "Bonds": 0.01, "Cash": 0.0}

optimal_path, total_cost = optimal_portfolio_rebalancing(
    current_portfolio,
    target_portfolio,
    transaction_costs
)

if optimal_path:
    print(f"Optimal rebalancing path with total cost {total_cost:.4f}:")
    for i, allocation in enumerate(optimal_path):
        print(f"Step {i}: {allocation}")
else:
    print("No valid path found")
```

## 3. Optimal Trading Execution with Time-Varying Costs

This example uses Bellman-Ford to determine the optimal trade execution strategy over time when costs vary:

```python
def optimal_trade_execution(total_shares, max_days, market_impact_model, time_varying_costs):
    """
    Find the optimal execution schedule for a large trade to minimize market impact

    Args:
        total_shares: Total number of shares to trade
        max_days: Maximum number of days to execute the trade
        market_impact_model: Function that calculates impact given shares traded
        time_varying_costs: Dictionary of time-specific costs

    Returns:
        Optimal execution schedule
    """
    # Generate possible states (shares remaining, day)
    states = []
    for day in range(max_days + 1):
        for shares in range(total_shares + 1):
            states.append((shares, day))

    # Build graph
    graph = {}
    for shares, day in states:
        if day < max_days:
            graph[(shares, day)] = {}
            # Try different amounts to trade today
            for trade_amount in range(shares + 1):
                new_state = (shares - trade_amount, day + 1)

                # Calculate cost using market impact model
                daily_cost = time_varying_costs.get(day, 0)
                impact_cost = market_impact_model(trade_amount)
                total_cost = impact_cost + daily_cost

                graph[(shares, day)][new_state] = total_cost

    # Run Bellman-Ford
    start_state = (total_shares, 0)
    distances = {start_state: 0}
    predecessors = {start_state: None}

    for _ in range(len(states) - 1):
        for u in states:
            if u in graph and u in distances:
                for v, weight in graph[u].items():
                    if v not in distances or distances[u] + weight < distances[v]:
                        distances[v] = distances[u] + weight
                        predecessors[v] = u

    # Find best end state (the one with 0 shares remaining)
    best_end_state = None
    min_cost = float('infinity')

    for state in states:
        shares, day = state
        if shares == 0 and state in distances and distances[state] < min_cost:
            min_cost = distances[state]
            best_end_state = state

    if best_end_state is None:
        return None, float('infinity')

    # Reconstruct path
    path = []
    current = best_end_state
    while current is not None:
        path.append(current)
        current = predecessors.get(current)

    path.reverse()

    # Convert to execution schedule
    schedule = []
    for i in range(len(path) - 1):
        current_shares, current_day = path[i]
        next_shares, next_day = path[i+1]
        shares_traded = current_shares - next_shares
        schedule.append((current_day, shares_traded))

    return schedule, min_cost

# Example usage
def simple_market_impact(shares):
    """Simple market impact model - cost increases with square of trade size"""
    return 0.01 * (shares ** 2)

# Time-varying costs (e.g., higher volatility on certain days)
time_costs = {
    0: 0.001,  # Monday
    1: 0.002,  # Tuesday
    2: 0.005,  # Wednesday (high volatility)
    3: 0.003,  # Thursday
    4: 0.001   # Friday
}

schedule, total_cost = optimal_trade_execution(
    total_shares=1000,
    max_days=5,
    market_impact_model=simple_market_impact,
    time_varying_costs=time_costs
)

if schedule:
    print(f"Optimal trading schedule with total cost {total_cost:.4f}:")
    days = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"]
    for day, shares in schedule:
        print(f"{days[day]}: Trade {shares} shares")
else:
    print("No valid execution schedule found")
```

## 4. Limit Order Book Path Analysis

This example analyzes the optimal path through a limit order book to execute a large trade:

```python
def optimal_order_execution(order_books, trade_size, transaction_fee_model):
    """
    Find the optimal path through multiple exchanges/order books

    Args:
        order_books: Dictionary mapping venue to their order book
        trade_size: Total size of trade to execute
        transaction_fee_model: Function to calculate fees

    Returns:
        Optimal execution strategy across venues
    """
    venues = list(order_books.keys())

    # Create states (remaining size, current venue)
    states = []
    for size in range(trade_size + 1):
        for venue in venues:
            states.append((size, venue))
    states.append((0, None))  # Final state

    # Build graph
    graph = {}
    for size, venue in states:
        if size > 0:  # If we still have shares to trade
            graph[(size, venue)] = {}

            # Option 1: Trade at current venue
            for execution_size in range(1, size + 1):
                # Check if order book has enough liquidity
                if execution_size <= len(order_books[venue]):
                    # Calculate execution cost using order book
                    execution_cost = sum(price for price, _ in order_books[venue][:execution_size])
                    fee = transaction_fee_model(venue, execution_size, execution_cost)
                    total_cost = execution_cost + fee

                    # Add edge to graph
                    new_state = (size - execution_size, venue)
                    graph[(size, venue)][new_state] = total_cost

            # Option 2: Switch venue
            for new_venue in venues:
                if new_venue != venue:
                    # Cost to switch venues (could be a fixed fee)
                    switch_cost = 0.1  # Example fixed cost
                    graph[(size, venue)][(size, new_venue)] = switch_cost

            # Option 3: Complete the trade (if all shares are executed)
            if size == 0:
                graph[(size, venue)][(0, None)] = 0

    # Run Bellman-Ford
    initial_venues = venues[0]  # Start at first venue
    start_state = (trade_size, initial_venues)
    end_state = (0, None)

    distances = {start_state: 0}
    predecessors = {start_state: None}

    for _ in range(len(states) - 1):
        for u in states:
            if u in graph and u in distances:
                for v, weight in graph[u].items():
                    if v not in distances or distances[u] + weight < distances[v]:
                        distances[v] = distances[u] + weight
                        predecessors[v] = u

    # Check if we can reach the end state
    if end_state not in distances:
        return None, float('infinity')

    # Reconstruct path
    path = []
    current = end_state
    while current is not None:
        path.append(current)
        current = predecessors.get(current)

    path.reverse()

    # Convert to execution strategy
    strategy = []
    for i in range(len(path) - 1):
        current_size, current_venue = path[i]
        next_size, next_venue = path[i+1]

        if current_venue != next_venue:
            if next_venue is not None:
                strategy.append(f"Switch from {current_venue} to {next_venue}")
        else:
            shares_executed = current_size - next_size
            if shares_executed > 0:
                strategy.append(f"Execute {shares_executed} shares at {current_venue}")

    return strategy, distances[end_state]

# Example usage
order_books = {
    "Exchange A": [(100.0, 100), (100.1, 200), (100.2, 300)],  # (price, size) pairs
    "Exchange B": [(100.2, 150), (100.3, 250), (100.4, 200)],
    "Exchange C": [(100.1, 120), (100.2, 180), (100.3, 300)]
}

def fee_model(venue, size, cost):
    """Simple fee model based on venue and trade size"""
    if venue == "Exchange A":
        return 0.002 * cost  # 0.2% fee
    elif venue == "Exchange B":
        return 0.001 * cost  # 0.1% fee
    else:
        return 0.0015 * cost  # 0.15% fee

strategy, total_cost = optimal_order_execution(
    order_books=order_books,
    trade_size=500,
    transaction_fee_model=fee_model
)

if strategy:
    print(f"Optimal execution strategy with total cost {total_cost:.4f}:")
    for step in strategy:
        print(step)
else:
    print("No valid execution strategy found")
```

## 5. Risk Arbitrage in Merger Scenarios

This example uses Bellman-Ford to analyze risk arbitrage opportunities in corporate mergers:

```python
def analyze_merger_arbitrage(securities, conversion_ratios, transaction_costs):
    """
    Analyze merger arbitrage opportunities across related securities

    Args:
        securities: Dictionary mapping security IDs to current prices
        conversion_ratios: Dictionary mapping (from_security, to_security) to conversion ratio
        transaction_costs: Dictionary mapping security to transaction cost percentage

    Returns:
        Arbitrage opportunity if it exists
    """
    # Build graph where:
    # - Vertices are securities
    # - Edges represent conversions or transactions with costs as weights
    securities_list = list(securities.keys())

    # Create graph
    graph = {sec: {} for sec in securities_list}

    # Add edges for conversions and direct trades
    for from_sec in securities_list:
        for to_sec in securities_list:
            if from_sec != to_sec:
                # Direct purchase/sale
                price_ratio = securities[from_sec] / securities[to_sec]
                cost_pct = transaction_costs.get(from_sec, 0.01) + transaction_costs.get(to_sec, 0.01)
                cost = -math.log(price_ratio * (1 - cost_pct))  # Negative log for Bellman-Ford
                graph[from_sec][to_sec] = cost

                # If there's a conversion ratio (e.g., in a merger scenario)
                if (from_sec, to_sec) in conversion_ratios:
                    conv_ratio = conversion_ratios[(from_sec, to_sec)]
                    # Calculate value after conversion including costs
                    value_ratio = (conv_ratio * securities[to_sec]) / securities[from_sec]
                    conv_cost = transaction_costs.get((from_sec, to_sec), 0.005)  # Conversion cost
                    effective_ratio = value_ratio * (1 - conv_cost)

                    # Use negative log for Bellman-Ford
                    weight = -math.log(effective_ratio)
                    graph[from_sec][to_sec] = min(graph[from_sec][to_sec], weight)

    # Run Bellman-Ford from each security to find negative cycles
    for source in securities_list:
        distances = {sec: float('infinity') for sec in securities_list}
        predecessors = {sec: None for sec in securities_list}
        distances[source] = 0

        # Relax edges
        for _ in range(len(securities_list) - 1):
            for u in securities_list:
                for v, weight in graph[u].items():
                    if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                        distances[v] = distances[u] + weight
                        predecessors[v] = u

        # Check for negative cycles
        for u in securities_list:
            for v, weight in graph[u].items():
                if distances[u] != float('infinity') and distances[u] + weight < distances[v]:
                    # Found negative cycle, extract it
                    cycle = []
                    visited = set()
                    current = u

                    while current not in visited:
                        visited.add(current)
                        cycle.append(current)
                        current = predecessors[current]

                    # Complete the cycle
                    start_idx = cycle.index(current)
                    arb_cycle = cycle[start_idx:] + cycle[:start_idx+1]

                    # Calculate profit
                    profit_factor = 1.0
                    for i in range(len(arb_cycle) - 1):
                        from_sec, to_sec = arb_cycle[i], arb_cycle[i+1]
                        # Check if it's a conversion
                        if (from_sec, to_sec) in conversion_ratios:
                            ratio = conversion_ratios[(from_sec, to_sec)]
                            cost = transaction_costs.get((from_sec, to_sec), 0.005)
                            profit_factor *= ratio * (1 - cost)
                        else:
                            # Direct trade
                            price_ratio = securities[to_sec] / securities[from_sec]
                            cost_pct = transaction_costs.get(from_sec, 0.01) + transaction_costs.get(to_sec, 0.01)
                            profit_factor *= price_ratio * (1 - cost_pct)

                    return {
                        "arbitrage_cycle": arb_cycle,
                        "profit_factor": profit_factor,
                        "profit_percentage": (profit_factor - 1) * 100
                    }

    return None

# Example usage for a merger scenario
securities_prices = {
    "Target": 45.50,              # Target company in a merger
    "Acquirer": 80.25,            # Acquiring company
    "Target Option": 4.75,        # Options on target company
    "Acquirer Bond": 950.00,      # Bonds of acquirer
    "Merger ETF": 65.30           # ETF tracking merger companies
}

# Conversion ratios in the merger
conversion_ratios = {
    ("Target", "Acquirer"): 0.6,              # Each Target share converts to 0.6 Acquirer shares
    ("Target Option", "Target"): 10.0,        # Each option controls 10 shares
    ("Acquirer Bond", "Acquirer"): 12.0,      # Each bond converts to 12 shares
    ("Merger ETF", "Target"): 0.5,            # ETF composition
    ("Merger ETF", "Acquirer"): 0.3           # ETF composition
}

# Transaction costs for each security (%)
transaction_costs = {
    "Target": 0.01,               # 1% cost
    "Acquirer": 0.01,             # 1% cost
    "Target Option": 0.02,        # 2% cost (options more expensive)
    "Acquirer Bond": 0.015,       # 1.5% cost
    "Merger ETF": 0.005,          # 0.5% cost
    # Conversion costs
    ("Target", "Acquirer"): 0.003,            # 0.3% conversion cost
    ("Target Option", "Target"): 0.01,        # 1% exercise cost
    ("Acquirer Bond", "Acquirer"): 0.005,     # 0.5% conversion cost
}

arbitrage = analyze_merger_arbitrage(
    securities_prices,
    conversion_ratios,
    transaction_costs
)

if arbitrage:
    print(f"Arbitrage opportunity found!")
    print(f"Cycle: {' -> '.join(arbitrage['arbitrage_cycle'])}")
    print(f"Profit factor: {arbitrage['profit_factor']:.4f}")
    print(f"Profit percentage: {arbitrage['profit_percentage']:.2f}%")
else:
    print("No arbitrage opportunity found - market is efficient")
```

Each of these examples demonstrates how the Bellman-Ford algorithm can be effectively applied to different financial problems. The algorithm's ability to handle negative weights and detect negative cycles makes it particularly valuable in financial applications where finding arbitrage opportunities or optimal trading paths is critical.

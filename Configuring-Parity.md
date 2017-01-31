# Configuring Parity

Parity can be configured using either the [CLI options](#cli-options) or a [config file](#config-file). Should the CLI flags and the config file disagree about a setting, the CLI takes precedence.

You can list all CLI options by running `$parity --help`. Each CLI option maps to a setting in the TOML file, for example `--mode-timeout 500` can be set by creating a config file:

```toml
[parity]
mode_timeout = 500
```

## Config File

Parity can be configured using a [TOML](https://github.com/toml-lang/toml) file. The file can be generated using the [Parity Config Generator](https://ethcore.github.io/parity-config-generator/). To start parity with a config file, the file needs to be located in:

* Windows: `%UserProfile%\AppData\Roaming\Parity\Ethereum\config.toml`
* Linux: `~/.local/share/io.parity.ethereum/config.toml`
* macOS: `$HOME/Library/Application Support/io.parity.ethereum/config.toml`

To use a custom path run `$ parity --config path/to/config.toml`.

## Default config.toml

The following is a representation of a configuration file with all default values.

```toml
[parity]
mode = "last"
mode_timeout = 300
mode_alarm = 3600
auto_update = "none"
release_track = "current"
no_download = false
no_consensus = false

chain = "homestead"
base_path = "$HOME/.parity"
db_path = "$HOME/.parity/chains"
keys_path = "$HOME/.parity/keys"
identity = ""
light = false

[account]
unlock = ["0xdeadbeefcafe0000000000000000000000000000"]
password = ["~/.safe/password.file"]
keys_iterations = 10240

[ui]
force = false
disable = false
port = 8180
interface = "127.0.0.1"
path = "$HOME/.parity/signer"

[network]
disable = false
port = 30303
min_peers = 25
max_peers = 50
nat = "any"
id = 1
bootnodes = []
discovery = true
warp = true
allow_ips = "all"
snapshot_peers = 0
max_pending_peers = 64
serve_light = true

reserved_only = false
reserved_peers = "./path_to_file"

[rpc]
disable = false
port = 8545
interface = "local"
cors = "null"
apis = ["web3", "eth", "net", "parity", "traces", "rpc"]
hosts = ["none"]

[ipc]
disable = false
path = "$HOME/.parity/jsonrpc.ipc"
apis = ["web3", "eth", "net", "parity", "parity_accounts", "personal", "traces", "rpc"]

[dapps]
disable = false
port = 8080
interface = "local"
hosts = ["none"]
path = "$HOME/.parity/dapps"
# authorization:
user = "test_user"
pass = "test_pass"

fengine_signer = "0xdeadbeefcafe0000000000000000000000000001"
force_sealing = true
reseal_on_txs = "all"
reseal_min_period = 4000
work_queue_size = 20
relay_set = "cheap"
usd_per_tx = "0.0025"
usd_per_eth = "auto"
price_update_period = "hourly"
gas_floor_target = "4700000"
gas_cap = "6283184"
tx_queue_size = 1024
tx_queue_gas = "auto"
tx_queue_strategy = "gas_factor"
tx_queue_ban_count = 1
tx_queue_ban_time = 180 #s
tx_gas_limit = "6283184"
tx_time_limit = 100 #ms
extra_data = "Parity"
remove_solved = false
notify_work = ["http://localhost:3001"]
refuse_service_transactions = false

[footprint]
tracing = "auto"
pruning = "auto"
pruning_history = 1200
pruning_memory = 500
cache_size_db = 64
cache_size_blocks = 8
cache_size_queue = 50
cache_size_state = 25
cache_size = 128 # Overrides above caches with total size
fast_and_loose = false
db_compaction = "ssd"
fat_db = "auto"
scale_verifiers = true
num_verifiers = 6

[snapshots]
disable_periodic = false

[vm]
jit = false

[misc]
logging = "own_tx=trace"
log_file = "/var/log/parity.log"
color = true
```


## CLI Options

```
Operating Options:
  --mode MODE                    Set the operating mode. MODE can be one of:
                                 last - Uses the last-used mode, active if none.
                                 active - Parity continuously syncs the chain.
                                 passive - Parity syncs initially, then sleeps and
                                 wakes regularly to resync.
                                 dark - Parity syncs only when the RPC is active.
                                 offline - Parity doesn't sync. (default: last).
  --mode-timeout SECS            Specify the number of seconds before inactivity
                                 timeout occurs when mode is dark or passive
                                 (default: 300).
  --mode-alarm SECS              Specify the number of seconds before auto sleep
                                 reawake timeout occurs when mode is passive
                                 (default: 3600).
  --auto-update SET              Set a releases set to automatically update and
                                 install.
                                 all - All updates in the our release track.
                                 critical - Only consensus/security updates.
                                 none - No updates will be auto-installed.
                                 (default: critical).
  --release-track TRACK          Set which release track we should use for updates.
                                 stable - Stable releases.
                                 beta - Beta releases.
                                 nightly - Nightly releases (unstable).
                                 testing - Testing releases (do not use).
                                 current - Whatever track this executable was
                                 released on (default: current).
  --no-download                  Normally new releases will be downloaded ready for
                                 updating. This disables it. Not recommended.
                                 (default: false).
  --no-consensus                 Force the binary to run even if there are known
                                 issues regarding consensus. Not recommended.
                                 (default: false).
  --force-direct                 Run the originally installed version of Parity,
                                 ignoring any updates that have since been installed.
  --chain CHAIN                  Specify the blockchain type. CHAIN may be either a
                                 JSON chain specification file or olympic, frontier,
                                 homestead, mainnet, morden, ropsten, classic, expanse,
                                 testnet or dev (default: homestead).
  -d --base-path PATH            Specify the base data storage path.
                                 (default: /home/maciej/.local/share/io.parity.ethereum).
  --db-path PATH                 Specify the database directory path
                                 (default: $BASE/chains).
  --keys-path PATH               Specify the path for JSON key files to be found
                                 (default: $BASE/keys).
  --identity NAME                Specify your node's name. (default: )

Account Options:
  --unlock ACCOUNTS              Unlock ACCOUNTS for the duration of the execution.
                                 ACCOUNTS is a comma-delimited list of addresses.
                                 Implies --no-ui. (default: None)
  --password FILE                Provide a file containing a password for unlocking
                                 an account. Leading and trailing whitespace is trimmed.
                                 (default: [])
  --keys-iterations NUM          Specify the number of iterations to use when
                                 deriving key from the password (bigger is more
                                 secure) (default: 10240).

UI Options:
  --force-ui                     Enable Trusted UI WebSocket endpoint,
                                 even when --unlock is in use. (default: $false)
  --no-ui                        Disable Trusted UI WebSocket endpoint.
                                 (default: $false)
  --ui-port PORT                 Specify the port of Trusted UI server
                                 (default: 8180).
  --ui-interface IP              Specify the hostname portion of the Trusted UI
                                 server, IP should be an interface's IP address,
                                 or local (default: local).
  --ui-path PATH                 Specify directory where Trusted UIs tokens should
                                 be stored. (default: $BASE/signer)
  --ui-no-validation             Disable Origin and Host headers validation for
                                 Trusted UI. WARNING: INSECURE. Used only for
                                 development. (default: false)

Networking Options:
  --warp                         Enable syncing from the snapshot over the network. (default: false)
  --port PORT                    Override the port on which the node should listen
                                 (default: 30303).
  --min-peers NUM                Try to maintain at least NUM peers (default: 25).
  --max-peers NUM                Allow up to NUM peers (default: 50).
  --snapshot-peers NUM           Allow additional NUM peers for a snapshot sync
                                 (default: 0).
  --nat METHOD                   Specify method to use for determining public
                                 address. Must be one of: any, none, upnp,
                                 extip:<IP> (default: any).
  --network-id INDEX             Override the network identifier from the chain we
                                 are on. (default: None)
  --bootnodes NODES              Override the bootnodes from our chain. NODES should
                                 be comma-delimited enodes. (default: None)
  --no-discovery                 Disable new peer discovery. (default: false)
  --node-key KEY                 Specify node secret key, either as 64-character hex
                                 string or input to SHA3 operation. (default: None)
  --reserved-peers FILE          Provide a file containing enodes, one per line.
                                 These nodes will always have a reserved slot on top
                                 of the normal maximum peers. (default: None)
  --reserved-only                Connect only to reserved nodes. (default: false)
  --allow-ips FILTER             Filter outbound connections. Must be one of:
                                 private - connect to private network IP addresses only;
                                 public - connect to public network IP addresses only;
                                 all - connect to any IP address.
                                 (default: all)
  --max-pending-peers NUM        Allow up to NUM pending connections. (default: 64)
  --no-ancient-blocks            Disable downloading old blocks after snapshot restoration
                                 or warp sync. (default: false)

API and Console Options:
  --no-jsonrpc                   Disable the JSON-RPC API server. (default: false)
  --jsonrpc-port PORT            Specify the port portion of the JSONRPC API server
                                 (default: 8545).
  --jsonrpc-interface IP         Specify the hostname portion of the JSONRPC API
                                 server, IP should be an interface's IP address, or
                                 all (all interfaces) or local (default: local).
  --jsonrpc-cors URL             Specify CORS header for JSON-RPC API responses.
                                 (default: None)
  --jsonrpc-apis APIS            Specify the APIs available through the JSONRPC
                                 interface. APIS is a comma-delimited list of API
                                 name. Possible name are web3, eth, net, personal,
                                 parity, parity_set, traces, rpc, parity_accounts.
                                 (default: web3,eth,net,parity,traces,rpc).
  --jsonrpc-hosts HOSTS          List of allowed Host header values. This option will
                                 validate the Host header sent by the browser, it
                                 is additional security against some attack
                                 vectors. Special options: "all", "none",
                                 (default: none).

  --no-ipc                       Disable JSON-RPC over IPC service. (default: false)
  --ipc-path PATH                Specify custom path for JSON-RPC over IPC service
                                 (default: $BASE/jsonrpc.ipc).
  --ipc-apis APIS                Specify custom API set available via JSON-RPC over
                                 IPC (default: web3,eth,net,parity,parity_accounts,traces,rpc).

  --no-dapps                     Disable the Dapps server (e.g. status page). (default: false)
  --dapps-port PORT              Specify the port portion of the Dapps server
                                 (default: 8080).
  --dapps-interface IP           Specify the hostname portion of the Dapps
                                 server, IP should be an interface's IP address,
                                 or local (default: local).
  --dapps-hosts HOSTS            List of allowed Host header values. This option will
                                 validate the Host header sent by the browser, it
                                 is additional security against some attack
                                 vectors. Special options: "all", "none",
                                 (default: none).
  --dapps-user USERNAME          Specify username for Dapps server. It will be
                                 used in HTTP Basic Authentication Scheme.
                                 If --dapps-pass is not specified you will be
                                 asked for password on startup. (default: None)
  --dapps-pass PASSWORD          Specify password for Dapps server. Use only in
                                 conjunction with --dapps-user. (default: None)
  --dapps-path PATH              Specify directory where dapps should be installed.
                                 (default: $BASE/dapps)
  --dapps-apis-all               Expose all possible RPC APIs on Dapps port.
                                 WARNING: INSECURE. Used only for development.
                                 (default: false)

Sealing/Mining Options:
  --author ADDRESS               Specify the block author (aka "coinbase") address
                                 for sending block rewards from sealed blocks.
                                 NOTE: MINING WILL NOT WORK WITHOUT THIS OPTION.
                                 (default: None)
  --engine-signer ADDRESS        Specify the address which should be used to
                                 sign consensus messages and issue blocks.
                                 Relevant only to non-PoW chains.
                                 (default: None)
  --force-sealing                Force the node to author new blocks as if it were
                                 always sealing/mining.
                                 (default: false)
  --reseal-on-txs SET            Specify which transactions should force the node
                                 to reseal a block. SET is one of:
                                 none - never reseal on new transactions;
                                 own - reseal only on a new local transaction;
                                 ext - reseal only on a new external transaction;
                                 all - reseal on all new transactions
                                 (default: own).
  --reseal-min-period MS         Specify the minimum time between reseals from
                                 incoming transactions. MS is time measured in
                                 milliseconds (default: 2000).
  --work-queue-size ITEMS        Specify the number of historical work packages
                                 which are kept cached lest a solution is found for
                                 them later. High values take more memory but result
                                 in fewer unusable solutions (default: 20).
  --tx-gas-limit GAS             Apply a limit of GAS as the maximum amount of gas
                                 a single transaction may have for it to be mined.
                                 (default: None)
  --tx-time-limit MS             Maximal time for processing single transaction.
                                 If enabled senders/recipients/code of transactions
                                 offending the limit will be banned from being included
                                 in transaction queue for 180 seconds.
                                 (default: None)
  --relay-set SET                Set of transactions to relay. SET may be:
                                 cheap - Relay any transaction in the queue (this
                                 may include invalid transactions);
                                 strict - Relay only executed transactions (this
                                 guarantees we don't relay invalid transactions, but
                                 means we relay nothing if not mining);
                                 lenient - Same as strict when mining, and cheap
                                 when not (default: cheap).
  --usd-per-tx USD               Amount of USD to be paid for a basic transaction
                                 (default: 0.0025). The minimum gas price is set
                                 accordingly.
  --usd-per-eth SOURCE           USD value of a single ETH. SOURCE may be either an
                                 amount in USD, a web service or 'auto' to use each
                                 web service in turn and fallback on the last known
                                 good value (default: auto).
  --price-update-period T        T will be allowed to pass between each gas price
                                 update. T may be daily, hourly, a number of seconds,
                                 or a time string of the form "2 days", "30 minutes"
                                 etc. (default: hourly).
  --gas-floor-target GAS         Amount of gas per block to target when sealing a new
                                 block (default: 4700000).
  --gas-cap GAS                  A cap on how large we will raise the gas limit per
                                 block due to transaction volume (default: 6283184).
  --extra-data STRING            Specify a custom extra-data for authored blocks, no
                                 more than 32 characters. (default: None)
  --tx-queue-size LIMIT          Maximum amount of transactions in the queue (waiting
                                 to be included in next block) (default: 1024).
  --tx-queue-gas LIMIT           Maximum amount of total gas for external transactions in
                                 the queue. LIMIT can be either an amount of gas or
                                 'auto' or 'off'. 'auto' sets the limit to be 20x
                                 the current block gas limit. (default: auto).
  --tx-queue-strategy S          Prioritization strategy used to order transactions
                                 in the queue. S may be:
                                 gas - Prioritize txs with low gas limit;
                                 gas_price - Prioritize txs with high gas price;
                                 gas_factor - Prioritize txs using gas price
                                 and gas limit ratio (default: gas_price).
  --tx-queue-ban-count C         Number of times maximal time for execution (--tx-time-limit)
                                 can be exceeded before banning sender/recipient/code.
                                 (default: 1)
  --tx-queue-ban-time SEC        Banning time (in seconds) for offenders of specified
                                 execution time limit. Also number of offending actions
                                 have to reach the threshold within that time.
                                 (default: 180 seconds)
  --remove-solved                Move solved blocks from the work package queue
                                 instead of cloning them. This gives a slightly
                                 faster import speed, but means that extra solutions
                                 submitted for the same work package will go unused.
                                 (default: false)
  --notify-work URLS             URLs to which work package notifications are pushed.
                                 URLS should be a comma-delimited list of HTTP URLs.
                                 (default: None)
  --refuse-service-transactions  Always refuse service transactions.
                                 (default: false).
  --stratum                      Run Stratum server for miner push notification. (default: false)
  --stratum-interface IP         Interface address for Stratum server. (default: local)
  --stratum-port PORT            Port for Stratum server to listen on. (default: 8008)
  --stratum-secret STRING        Secret for authorizing Stratum server for peers.
                                 (default: None)

Footprint Options:
  --tracing BOOL                 Indicates if full transaction tracing should be
                                 enabled. Works only if client had been fully synced
                                 with tracing enabled. BOOL may be one of auto, on,
                                 off. auto uses last used value of this option (off
                                 if it does not exist) (default: auto).
  --pruning METHOD               Configure pruning of the state/storage trie. METHOD
                                 may be one of auto, archive, fast:
                                 archive - keep all state trie data. No pruning.
                                 fast - maintain journal overlay. Fast but 50MB used.
                                 auto - use the method most recently synced or
                                 default to fast if none synced (default: auto).
  --pruning-history NUM          Set a minimum number of recent states to keep when pruning
                                 is active. (default: 1200).
  --pruning-memory MB            The ideal amount of memory in megabytes to use to store
                                 recent states. As many states as possible will be kept
                                 within this limit, and at least --pruning-history states
                                 will always be kept. (default: 150)
  --cache-size-db MB             Override database cache size (default: 64).
  --cache-size-blocks MB         Specify the prefered size of the blockchain cache in
                                 megabytes (default: 8).
  --cache-size-queue MB          Specify the maximum size of memory to use for block
                                 queue (default: 50).
  --cache-size-state MB          Specify the maximum size of memory to use for
                                 the state cache (default: 25).
  --cache-size MB                Set total amount of discretionary memory to use for
                                 the entire system, overrides other cache and queue
                                 options. (default: None)
  --fast-and-loose               Disables DB WAL, which gives a significant speed up
                                 but means an unclean exit is unrecoverable. (default: false)
  --db-compaction TYPE           Database compaction type. TYPE may be one of:
                                 ssd - suitable for SSDs and fast HDDs;
                                 hdd - suitable for slow HDDs;
                                 auto - determine automatically (default: auto).
  --fat-db BOOL                  Build appropriate information to allow enumeration
                                 of all accounts and storage keys. Doubles the size
                                 of the state database. BOOL may be one of on, off
                                 or auto. (default: auto)
  --scale-verifiers              Automatically scale amount of verifier threads based on
                                 workload. Not guaranteed to be faster.
                                 (default: false)
  --num-verifiers INT            Amount of verifier threads to use or to begin with, if verifier
                                 auto-scaling is enabled. (default: None)

Import/Export Options:
  --from BLOCK                   Export from block BLOCK, which may be an index or
                                 hash (default: 1).
  --to BLOCK                     Export to (including) block BLOCK, which may be an
                                 index, hash or 'latest' (default: latest).
  --format FORMAT                For import/export in given format. FORMAT must be
                                 one of 'hex' and 'binary'.
                                 (default: None = Import: auto, Export: binary)
  --no-seal-check                Skip block seal check. (default: false)
  --at BLOCK                     Export state at the given block, which may be an
                                 index, hash, or 'latest'. (default: latest)
  --no-storage                   Don't export account storage. (default: false)
  --no-code                      Don't export account code. (default: false)
  --min-balance WEI              Don't export accounts with balance less than specified.
                                 (default: None)
  --max-balance WEI              Don't export accounts with balance greater than specified.
                                 (default: None)

Snapshot Options:
  --at BLOCK                     Take a snapshot at the given block, which may be an
                                 index, hash, or 'latest'. Note that taking snapshots at
                                 non-recent blocks will only work with --pruning archive
                                 (default: latest)
  --no-periodic-snapshot         Disable automated snapshots which usually occur once
                                 every 10000 blocks. (default: false)

Virtual Machine Options:
  --jitvm                        Enable the JIT VM. (default: false)

Legacy Options:
  --geth                         Run in Geth-compatibility mode. Sets the IPC path
                                 to be the same as Geth's. Overrides the --ipc-path
                                 and --ipcpath options. Alters RPCs to reflect Geth
                                 bugs. Includes the personal_ RPC by default.
  --testnet                      Geth-compatible testnet mode. Equivalent to --chain
                                 testnet --keys-path $HOME/parity/testnet-keys.
                                 Overrides the --keys-path option.
  --import-geth-keys             Attempt to import keys from Geth client.
  --datadir PATH                 Equivalent to --base-path PATH.
  --networkid INDEX              Equivalent to --network-id INDEX.
  --peers NUM                    Equivalent to --min-peers NUM.
  --nodekey KEY                  Equivalent to --node-key KEY.
  --nodiscover                   Equivalent to --no-discovery.
  -j --jsonrpc                   Does nothing; JSON-RPC is on by default now.
  --jsonrpc-off                  Equivalent to --no-jsonrpc.
  -w --webapp                    Does nothing; dapps server is on by default now.
  --dapps-off                    Equivalent to --no-dapps.
  --rpc                          Does nothing; JSON-RPC is on by default now.
  --rpcaddr IP                   Equivalent to --jsonrpc-interface IP.
  --rpcport PORT                 Equivalent to --jsonrpc-port PORT.
  --rpcapi APIS                  Equivalent to --jsonrpc-apis APIS.
  --rpccorsdomain URL            Equivalent to --jsonrpc-cors URL.
  --ipcdisable                   Equivalent to --no-ipc.
  --ipc-off                      Equivalent to --no-ipc.
  --ipcapi APIS                  Equivalent to --ipc-apis APIS.
  --ipcpath PATH                 Equivalent to --ipc-path PATH.
  --gasprice WEI                 Minimum amount of Wei per GAS to be paid for a
                                 transaction to be accepted for mining. Overrides
                                 --basic-tx-usd.
  --etherbase ADDRESS            Equivalent to --author ADDRESS.
  --extradata STRING             Equivalent to --extra-data STRING.
  --cache MB                     Equivalent to --cache-size MB.

Internal Options:
  --can-restart                  Executable will auto-restart if exiting with 69.

Miscellaneous Options:
  -c --config CONFIG             Specify a filename containing a configuration file.
                                 (default: $BASE/config.toml)
  -l --logging LOGGING           Specify the logging level. Must conform to the same
                                 format as RUST_LOG. (default: None)
  --log-file FILENAME            Specify a filename into which logging should be
                                 appended. (default: None)
  --no-config                    Don't load a configuration file.
  --no-color                     Don't use terminal color codes in output. (default: false)
  -v --version                   Show information about version.
  -h --help                      Show this screen.
```
> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveListStore` is the core module of **AtomicXCore** responsible for managing the live room list, creating and joining rooms, and maintaining room state. With LiveListStore, you can implement comprehensive live streaming lifecycle management in your application.

## Core Features
- **Live Room List Fetching**: Retrieve a paginated list of all currently public live rooms.

- **Live Lifecycle Management**: Provides a complete set of interfaces for the entire live streaming workflow, including room creation, going live, joining, leaving, and ending a live session.

- **Real-Time Event Listening**: Listen for key events such as live session end or users being removed from a room.

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibility & Description** |
| --- | --- | --- |
| `LiveInfo` | `data class` | Represents the complete information model of a live room. Includes the live room ID (liveID), name (liveName), owner information (liveOwner), and custom metadata (metaData), among other properties. |
| `LiveListState` | `data class` | Represents the current state of the live list module. The core property liveList is a StateFlow containing the fetched live room list; currentLive represents the information of the live room the user is currently in. |
| `LiveListListener` | `abstract class` | Handles global live room events, including onLiveEnded (live ended) and onKickedOutOfLive (user removed from live), for responding to key room state changes. |
| `LiveListStore` | `abstract class` | The core management class for interacting with the live room list and room lifecycle. It is a global singleton responsible for all operations such as creating, joining, and updating live room information. |

## Implementation

### Step 1: Component Integration
- **Video Live Streaming**：Refer to Quick Start to integrate AtomicXCore and complete the implementation of the Host Video Streaming and Audience Join and Watch features.

- **Voice Chat Room**：Refer to Quick Start to integrate AtomicXCore and complete the implementation of the Host Audio Streaming and Audience Join and Watch features.

### Step 2: Implement Audience Entry from Live Room List

Create a page to display the live room list using RecyclerView to layout live room cards. When a user taps a card, retrieve the liveId for that room and navigate to the audience viewing page.
``` kotlin
import android.content.Intent
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.GridLayoutManager
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

class LiveListActivity : AppCompatActivity() {
    private val liveListStore = LiveListStore.shared()
    private var liveList: List<LiveInfo> = emptyList()
    private val coroutineScope = CoroutineScope(Dispatchers.Main)

    private lateinit var recyclerView: RecyclerView
    private lateinit var adapter: LiveListAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_list)
        setupUI()
        bindStore()
        fetchLiveList()
    }

    private fun bindStore() {
        // Subscribe to the state to automatically receive list updates
        coroutineScope.launch {
            liveListStore.liveState.liveList.collect { fetchedList ->
                liveList = fetchedList
                adapter.notifyDataSetChanged()
            }
        }
    }

    private fun fetchLiveList() {
        liveListStore.fetchLiveList(
            cursor = "",
            count = 20,
            completion = object : CompletionHandler {
                override fun onSuccess() {
                    println("Live room list fetched successfully")
                }

                override fun onFailure(code: Int, desc: String) {
                    println("Failed to fetch live room list: $desc")
                }
            }
        )
    }

    // When a user clicks an item in the list
    private fun onLiveItemClick(liveInfo: LiveInfo) {
        // Create the audience viewing page and pass the liveId
        val intent = Intent(this, YourAudienceActivity::class.java)
        intent.putExtra("liveId", liveInfo.liveID)
        startActivity(intent)
    }

    // --- RecyclerView related methods ---
    private fun setupUI() {
        recyclerView = findViewById(R.id.recyclerView)
        adapter = LiveListAdapter(liveList) { liveInfo ->
            onLiveItemClick(liveInfo)
        }
        recyclerView.layoutManager = GridLayoutManager(this, 2)
        recyclerView.adapter = adapter
    }

    override fun onDestroy() {
        super.onDestroy()
        coroutineScope.cancel()
    }
}

// RecyclerView Adapter
class LiveListAdapter(
    private var liveList: List<LiveInfo>,
    private val onItemClick: (LiveInfo) -> Unit
) : RecyclerView.Adapter<LiveListAdapter.LiveViewHolder>() {

    class LiveViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        // Define your ViewHolder view components
        // val titleTextView: TextView = itemView.findViewById(R.id.titleTextView)
        // val coverImageView: ImageView = itemView.findViewById(R.id.coverImageView)
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): LiveViewHolder {
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.item_live_card, parent, false)
        return LiveViewHolder(view)
    }

    override fun onBindViewHolder(holder: LiveViewHolder, position: Int) {
        val liveInfo = liveList[position]
        // Set data to ViewHolder
        // holder.titleTextView.text = liveInfo.liveName
        // Load cover image, etc.

        holder.itemView.setOnClickListener {
            onItemClick(liveInfo)
        }
    }

    override fun getItemCount(): Int = liveList.size
}
```

#### LiveInfo Parameter Reference
| **Parameter Name** | **Type** | **Description** |
| --- | --- | --- |
| `liveID` | `String` | Unique identifier for the live room |
| `liveName` | `String` | Title of the live room |
| `coverURL` | `String` | Cover image URL for the live room |
| `liveOwner` | [LiveUserInfo](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-user-info/index.html) | Personal information of the room owner |
| `totalViewerCount` | `Int` | Total number of viewers in the live room |
| `categoryList` | `List<Int>` | List of category tags for the live room |
| `notice` | `String` | Announcement information for the live room |
| `metaData` | `Map<String, String>` | Developer-defined metadata for implementing advanced business scenarios |

## Advanced Features

### Scenario 1: Category Filtering for Live Room List

On the live plaza page, users can select category tags such as "Hot", "Music", "Games", etc. When a tag is selected, the live room list dynamically filters to display only rooms in the chosen category, helping users quickly discover relevant content.

#### Implementation

Use the `categoryList` property in the `LiveInfo` model. When the host selects a category while going live, the `fetchLiveList` API returns LiveInfo objects that include these category details. After retrieving the full live room list, filter it on the client based on the user’s selected category and refresh the UI.

#### Code Example

The following example shows how to extend a `LiveListManager` within `LiveListActivity` to handle data retrieval and filtering logic.
``` kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

// 1. Create a data manager to encapsulate data retrieval and filtering logic
class LiveListManager {
    private val liveListStore = LiveListStore.shared()
    private var fullLiveList: List<LiveInfo> = emptyList()

    // Expose the final filtered live list externally
    private val _filteredLiveList = MutableStateFlow<List<LiveInfo>>(emptyList())
    val filteredLiveList: StateFlow<List<LiveInfo>> = _filteredLiveList

    init {
        // Listen for full list changes
        CoroutineScope(Dispatchers.Main).launch {
            liveListStore.liveState.liveList.collect { fetchedList ->
                fullLiveList = fetchedList
                // By default, publish the complete list
                _filteredLiveList.value = fetchedList
            }
        }
    }

    fun fetchFirstPage() {
        liveListStore.fetchLiveList(cursor = "", count = 20, completion = null)
    }

    /// Filter the live list by category
    fun filterLiveList(categoryId: Int?) {
        if (categoryId == null) {
            // If categoryId is null, show the complete list
            _filteredLiveList.value = fullLiveList
            return
        }

        val filteredList = fullLiveList.filter { liveInfo ->
            liveInfo.categoryList.contains(categoryId)
        }
        _filteredLiveList.value = filteredList
    }
}

// 2. Use the Manager in your LiveListActivity
class LiveListActivity : AppCompatActivity() {
    private val manager = LiveListManager()
    private lateinit var recyclerView: RecyclerView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_list)
        // setupUI()

        // Bind data
        CoroutineScope(Dispatchers.Main).launch {
            manager.filteredLiveList.collect { filteredList ->
                // Refresh UI
               // adapter.updateList(filteredList)
            }
        }

        // Fetch first page
        manager.fetchFirstPage()
    }

    // When the user clicks a top category tag
    fun onCategorySelected(categoryId: Int) {
        manager.filterLiveList(categoryId)
    }

    // ... (RecyclerView related code)
}
```

### Scenario 2: Swipe-to-Play for Live Room List

Users can switch between live rooms by swiping up and down. When a new live room is centered on the screen, the video preview automatically starts playing. When it leaves the screen, playback stops automatically to save bandwidth and device resources.

> **Note：**
> 

> **Swipe-to-Play **is currently only supported for Video Live Streaming.
> 

#### Interaction Flow

#### Implementation

`LiveCoreView` supports multiple instances. Create a separate `LiveCoreView` for each `RecyclerView.ViewHolder`. By monitoring the scroll state of the `RecyclerView`, you can precisely control when to start or stop streaming in each ViewHolder, achieving "play on swipe in, stop on swipe out" behavior.

#### Code Example

We create a custom `LiveFeedViewHolder` that holds a `LiveCoreView` internally. We then manage the playback state of these ViewHolders in the `Activity`.
``` kotlin
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.view.CoreViewType
import io.trtc.tuikit.atomicxcore.api.view.LiveCoreView

// 1. Custom RecyclerView.ViewHolder, containing a LiveCoreView internally
class LiveFeedViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
    private var liveCoreView: LiveCoreView? = null
    
    fun setLiveInfo(liveInfo: LiveInfo) {
        // Create a new LiveCoreView for the new live info
        liveCoreView = LiveCoreView(itemView.context, viewType = CoreViewType.PLAY_VIEW)
        liveCoreView?.let { view ->
            (itemView as ViewGroup).addView(view)
            view.layoutParams = ViewGroup.LayoutParams(
                ViewGroup.LayoutParams.MATCH_PARENT,
                ViewGroup.LayoutParams.MATCH_PARENT
            )
        }
    }

    fun startPlay(roomId: String) {
        liveCoreView?.startPreviewLiveStream(roomId, false, callback = null)
    }
    
    fun stopPlay(roomId: String) {
        liveCoreView?.stopPreviewLiveStream(roomId)
    }
}

// 2. Manage playback logic in the Activity
class LiveFeedActivity : AppCompatActivity() {
    
    private lateinit var recyclerView: RecyclerView
    private var liveList: List<LiveInfo> = emptyList()
    private var currentPlayingPosition: Int = -1

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_feed)
        setupRecyclerView()
    }

    private fun setupRecyclerView() {
        recyclerView = findViewById(R.id.recyclerView)
        recyclerView.layoutManager = LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false)
        recyclerView.adapter = LiveFeedAdapter(liveList) { position ->
            playVideoAtPosition(position)
        }

        // Listen for scroll state
        recyclerView.addOnScrollListener(object : RecyclerView.OnScrollListener() {
            override fun onScrollStateChanged(recyclerView: RecyclerView, newState: Int) {
                super.onScrollStateChanged(recyclerView, newState)
                if (newState == RecyclerView.SCROLL_STATE_IDLE) {
                    val layoutManager = recyclerView.layoutManager as LinearLayoutManager
                    val firstVisiblePosition = layoutManager.findFirstCompletelyVisibleItemPosition()
                    if (firstVisiblePosition != RecyclerView.NO_POSITION) {
                        playVideoAtPosition(firstVisiblePosition)
                    }
                }
            }
        })
    }

    private fun playVideoAtPosition(position: Int) {
        // Only switch playback when the centered position changes
        if (currentPlayingPosition != position) {
            // Stop current playback
            if (currentPlayingPosition != -1) {
                val currentViewHolder = recyclerView.findViewHolderForAdapterPosition(currentPlayingPosition)
                if (currentViewHolder is LiveFeedViewHolder) {
                    val liveInfo = liveList[currentPlayingPosition]
                    currentViewHolder.stopPlay(liveInfo.liveID)
                }
            }
            
            // Start new playback
            val newViewHolder = recyclerView.findViewHolderForAdapterPosition(position)
            if (newViewHolder is LiveFeedViewHolder) {
                val liveInfo = liveList[position]
                newViewHolder.startPlay(liveInfo.liveID)
                currentPlayingPosition = position
            }
        }
    }
    
    // RecyclerView Adapter
    inner class LiveFeedAdapter(
        private var liveList: List<LiveInfo>,
        private val onItemClick: (Int) -> Unit
    ) : RecyclerView.Adapter<LiveFeedViewHolder>() {
        
        override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): LiveFeedViewHolder {
            val view = LayoutInflater.from(parent.context)
                .inflate(R.layout.item_live_feed, parent, false)
            return LiveFeedViewHolder(view)
        }

        override fun onBindViewHolder(holder: LiveFeedViewHolder, position: Int) {
            val liveInfo = liveList[position]
            holder.setLiveInfo(liveInfo)
            holder.itemView.setOnClickListener {
                onItemClick(position)
            }
        }

        override fun getItemCount(): Int = liveList.size
    }
}
```

## API Documentation

For detailed information on all public interfaces, properties, and methods of [LiveListStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) and related classes, refer to the official API documentation included with the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) framework. The relevant Stores used in this document are as follows:
| **Store/Component** | **Feature Description** | **API Documentation** |
| --- | --- | --- |
| LiveCoreView | Core view component for live video stream display and interaction. Responsible for video stream rendering and view widget handling, supporting scenarios such as host streaming, audience co-hosting, and host linking. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) |
| LiveListStore | Full lifecycle management of live rooms: create, join, leave, destroy rooms; query room list; modify live information (name, announcement, etc.); listen to live status (such as being removed or ended). | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) |

## FAQs

### Is the list data for voice chat rooms and video live rooms the same?

Yes. The data is unified; you do not need to fetch them separately. LiveListStore is a global singleton that manages the lifecycle of all "live" rooms in your application, including both video live rooms and voice chat rooms.

### How do I distinguish between voice chat rooms and video live rooms in the live room list?

`LiveListStore` does not differentiate between room business types. You must filter and categorize the list after fetching, at the application or UI layer.

We recommend two approaches:

**Approach 1 (Recommended): Use seatLayoutTemplateID for differentiation.**

This template ID defines the room layout. For supported template IDs and effects, refer to Run And Test.
- **Step 1: Specify ID when creating a room**

  - When calling `LiveListStore.shared.createLive`, set the `seatLayoutTemplateID` property of `LiveInfo` based on your business scenario:

  - Voice chat rooms: Use template IDs in the range 1–199.

  - Video live rooms: Use template IDs in the range 200–999.

- **Step 2: Filter when fetching the list**

  - On the client side, after receiving the list in `LiveListStore.state.liveList`, determine the business scenario by checking the template ID range.
      

      > **Note：**
      > 

      > If the seatLayoutTemplateID does not match your business scenario (voice chat room or video live room), seat layout features may not work as expected.
      > 

      **Approach 2:****Add a business prefix to **`liveID`**.**

      This is an optional, application-layer convention to help you filter rooms quickly.

- **Step 1: Add prefix when creating a room**

  - When generating liveID and calling createLive, assign different prefixes for each business type. For example: video live room IDs start with "Live_" (e.g., Live_12345), voice chat room IDs start with "voice_" (e.g., voice_67890).

- **Step 2: Check prefix when fetching the list**

  - On the client side, after fetching the list, distinguish rooms by checking the liveID prefix.

---

`LiveListStore` is the core module of **AtomicXCore** responsible for managing the live room list, creating and joining rooms, and maintaining room state. With `LiveListStore`, you can implement comprehensive live streaming lifecycle management in your application.

## Core Features
- **Live Room List Fetching**: Retrieve all currently public live rooms, returned one page at a time.

- **Live Lifecycle Management**: Provides a complete set of interfaces for the entire live streaming workflow, including room creation, going live, joining, leaving, and ending a live session.

- **Real-Time Event Listening**: Listen for key events such as live session end or users being removed from a room.

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibility & Description** |
| --- | --- | --- |
| `LiveInfo` | `struct` | - Represents the complete information model of a live room.  - Includes the live room ID (`liveID`), name (`liveName`), owner information (`liveOwner`), and custom metadata (`metaData`), among other properties. |
| `LiveListState` | `struct` | - Represents the current state of the live list module.  - The core property `liveList` is a StateFlow containing the fetched live room list;  - `currentLive` represents the information of the live room the user is currently in. |
| `LiveListEvent` | `enum` | Handles global live room events, including `.onLiveEnded` (live ended) and `.onKickedOutOfLive` (user removed from live), for responding to key room state changes. |
| `LiveListStore` | `class` | - The core management class for interacting with the live room list and room lifecycle.  - It is a global singleton responsible for all operations such as creating, joining, and updating live room information. |

## Implementation

### Step 1: Component Integration
- **Video Live Streaming**：Refer to Quick Start to integrate AtomicXCore and complete the implementation of the Host Video Streaming and Audience Join and Watch features.

- **Voice Chat Room**：Refer to Quick Start to integrate AtomicXCore and complete the implementation of the Host Audio Streaming and Audience Join and Watch features.

### Step 2: Implement Audience Entry from Live Room List

Create a page to display the live room list using `UICollectionView` to lay out live room cards. When a user taps a card, retrieve the `liveID` for that room and navigate to the audience viewing page.
``` swift
import AtomicXCore
import SnapKit
import RTCRoomEngine
import Combine

class LiveListViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate, UICollectionViewDelegateFlowLayout {

    private let liveListStore = LiveListStore.shared
    private var cancellables = Set<AnyCancellable>()
    private var liveList: [LiveInfo] = []
    private var collectionView: UICollectionView!

    override func viewDidLoad() {
        super.viewDidLoad()
        setupUI()
        bindStore()
        fetchLiveList()
    }
    
    private func bindStore() {
        // Subscribe to state to automatically receive list updates
        liveListStore.state
            .subscribe(StatePublisherSelector(keyPath: \LiveListState.liveList))
            .receive(on: DispatchQueue.main)
            .sink { [weak self] fetchedList in
                self?.liveList = fetchedList
                self?.collectionView.reloadData()
            }
            .store(in: &cancellables)
    }

    private func fetchLiveList() {
        liveListStore.fetchLiveList(cursor: "", count: 20) { result in
            if case .failure(let error) = result {
                print("Failed to fetch live room list: \(error.localizedDescription)")
            }
        }
    }
    
    // Called when the user taps a cell in the list
    func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
        let selectedLiveInfo = liveList[indexPath.item]
        // Create the audience viewing page and pass in the liveID
        let audienceVC = YourAudienceViewController(liveId: selectedLiveInfo.liveID)
        audienceVC.modalPresentationStyle = .fullScreen
        present(audienceVC, animated: true)
    }
    
    // --- UICollectionViewDataSource, Delegate, and UI setup methods ---
    private func setupUI() {
        let layout = UICollectionViewFlowLayout()
        // ... (Customize your layout as needed)
        collectionView = UICollectionView(frame: view.bounds, collectionViewLayout: layout)
        collectionView.dataSource = self
        collectionView.delegate = self
        collectionView.register(UICollectionViewCell.self, forCellWithReuseIdentifier: "LiveCell")
        view.addSubview(collectionView)
    }

    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return liveList.count
    }
    
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "LiveCell", for: indexPath)
        cell.backgroundColor = .lightGray // Customize your cell style
        // let liveInfo = liveList[indexPath.item]
        // ... (e.g.: cell.titleLabel.text = liveInfo.liveName)
        return cell
    }
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        // Adjust cell size for single or double column layout as needed
        let width = (view.bounds.width - 30) / 2
        return CGSize(width: width, height: width * 1.2)
    }
}
```

#### LiveInfo Parameter Reference
| **Parameter Name** | **Type** | **Description** |
| --- | --- | --- |
| `liveID` | `String` | Unique identifier for the live room |
| `liveName` | `String` | Title of the live room |
| `coverURL` | `String` | URL of the live room cover image |
| `liveOwner` | [LiveUserInfo](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveuserinfo) | Personal information of the room owner |
| `totalViewerCount` | `Int` | Total number of viewers in the live room |
| `categoryList` | `[NSNumber]` | List of category tags for the live room |
| `notice` | `String` | Announcement information for the live room |
| `metaData` | `[String: String]` | Developer-defined metadata for implementing complex business scenarios |

## Advanced Features

### Scenario 1: Category Filtering for Live Room List

On the live plaza page, users can select category tags such as "Hot", "Music", "Games", etc. When a tag is selected, the live room list dynamically filters to display only rooms in the chosen category, helping users quickly discover relevant content.

#### Implementation

Use the `categoryList` property in the `LiveInfo` model. When the host sets a category at the start of the stream, the `LiveInfo` object returned by `fetchLiveList` includes this category data. After fetching the full live room list, filter it on the client side based on the selected category and update the UI.

#### Code Example

The following example shows how to extend a `LiveListManager` in `LiveListViewController` to handle data fetching and category filtering:
``` swift
import AtomicXCore
import Combine

// 1. Data manager for fetching and filtering
class LiveListManager {
    private let liveListStore = LiveListStore.shared
    private var cancellables = Set<AnyCancellable>()
    private var fullLiveList: [LiveInfo] = []

    // Publisher for the filtered live list
    let filteredLiveListPublisher = CurrentValueSubject<[LiveInfo], Never>([])

    init() {
        liveListStore.state
            .subscribe(StatePublisherSelector(keyPath: \LiveListState.liveList))
            .receive(on: DispatchQueue.main)
            .sink { [weak self] fetchedList in
                self?.fullLiveList = fetchedList
                // By default, publish the complete list
                self?.filteredLiveListPublisher.send(fetchedList)
            }
            .store(in: &cancellables)
    }

    func fetchFirstPage() {
        liveListStore.fetchLiveList(cursor: "", count: 20) { _ in }
    }

    /// Filter the live list by category
    func filterLiveList(by categoryId: NSNumber?) {
        guard let categoryId = categoryId else {
            // Show the full list if no category is selected
            filteredLiveListPublisher.send(fullLiveList)
            return
        }
        let filteredList = fullLiveList.filter { liveInfo in
            liveInfo.categoryList.contains(categoryId)
        }
        filteredLiveListPublisher.send(filteredList)
    }
}

// 2. Use the manager in your LiveListViewController
class LiveListViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate {

    private let manager = LiveListManager()
    private var cancellables = Set<AnyCancellable>()
    private var liveList: [LiveInfo] = []
    private var collectionView: UICollectionView!

    override func viewDidLoad() {
        super.viewDidLoad()
        // ... setupUI ...

        // Bind data
        manager.filteredLiveListPublisher
            .receive(on: DispatchQueue.main)
            .sink { [weak self] filteredList in
                self?.liveList = filteredList
                self?.collectionView.reloadData()
            }
            .store(in: &cancellables)

        // Fetch the first page
        manager.fetchFirstPage()
    }

    // Handle category selection (e.g., UISegmentedControl)
    @objc func categorySegmentDidChange(_ sender: UISegmentedControl) {
        let selectedCategoryId: NSNumber? = 1 // Example: "Music" category ID is 1
        manager.filterLiveList(by: selectedCategoryId)
    }

    // ... (UICollectionView related code)
}
```

### Scenario 2: Swipe-to-Play for Live Room List

Users can switch between live rooms by swiping up or down. When a new live room is centered on the screen, its video will automatically start preview playback; when it is swiped away or no longer visible on the screen, playback will automatically stop to save bandwidth and device resources.

> **Note：**
> 

> **Swipe-to-Play **is currently only supported for Video Live Streaming.
> 

#### Interaction Flow

#### Implementation

`LiveCoreView` supports multiple instances. Create a separate `LiveCoreView` for each `UICollectionViewCell`. By listening to the scroll delegate methods of `UICollectionView`, you can control when the `LiveCoreView` in each cell should start or stop streaming, enabling "play on swipe in, stop on swipe out".

#### Code Example

Create a custom `LiveFeedCell` containing a `LiveCoreView`. Then, manage playback state in your view controller:
``` swift
import UIKit
import AtomicXCore

// 1. Custom UICollectionViewCell with LiveCoreView
class LiveFeedCell: UICollectionViewCell {
    private var liveCoreView: LiveCoreView?

    func setLiveInfo(_ liveInfo: LiveInfo) {
        // Create a new LiveCoreView for the new live info
        liveCoreView = LiveCoreView(viewType: .playView)
        guard let liveCoreView = liveCoreView else { return }
        contentView.addSubview(liveCoreView)
        liveCoreView.frame = contentView.bounds
    }

    func startPlay(roomId: String) {
        liveCoreView?.startPreviewLiveStream(roomId: roomId, isMuteAudio: false)
    }

    func stopPlay(roomId: String) {
        liveCoreView?.stopPreviewLiveStream(roomId: roomId)
    }
}

// 2. Manage playback in the ViewController
class LiveFeedViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate {

    private var collectionView: UICollectionView!
    private var liveList: [LiveInfo] = []
    private var currentPlayingIndexPath: IndexPath?

    // Called when scrolling stops
    func scrollViewDidEndDecelerating(_ scrollView: UIScrollView) {
        let page = Int(scrollView.contentOffset.y / view.frame.height)
        let indexPath = IndexPath(item: page, section: 0)
        // Switch playback only when the centered cell changes
        if currentPlayingIndexPath != indexPath {
            playVideo(at: indexPath)
        }
    }

    // Called when a cell is about to leave the screen
    func collectionView(_ collectionView: UICollectionView, didEndDisplaying cell: UICollectionViewCell, forItemAt indexPath: IndexPath) {
        if let liveCell = cell as? LiveFeedCell {
            let liveInfo = liveList[indexPath.item]
            liveCell.stopPlay(roomId: liveInfo.liveID)
        }
    }

    private func playVideo(at indexPath: IndexPath) {
        if let cell = collectionView.cellForItem(at: indexPath) as? LiveFeedCell {
            let liveInfo = liveList[indexPath.item]
            cell.startPlay(roomId: liveInfo.liveID)
            currentPlayingIndexPath = indexPath
        }
    }

    // ... (Other UICollectionViewDataSource methods)
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "LiveFeedCell", for: indexPath) as! LiveFeedCell
        cell.setLiveInfo(liveList[indexPath.item])
        return cell
    }
}
```

## **API Documentation**

For detailed information on all public interfaces, properties, and methods of [LiveListStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) and related classes, refer to the official API documentation included with the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) framework. The relevant Stores used in this document are as follows:
| **Store/Component** | **Feature Description** | **API Documentation** |
| --- | --- | --- |
| LiveCoreView | - Core view component for live video stream display and interaction.  - Responsible for video stream rendering and view widget handling, supporting scenarios such as host streaming, audience co-hosting, and host linking. | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview) |
| LiveListStore | Full lifecycle management of live rooms: create, join, leave, destroy rooms; query room list; modify live information (name, announcement, etc.); listen to live status (such as being removed or ended). | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) |

## FAQs

### Is the list data for voice chat rooms and video live rooms the same?

Yes. The data is unified; you do not need to fetch them separately. `LiveListStore` is a global singleton that manages the lifecycle of all "live" rooms in your application, including both video live rooms and voice chat rooms.

### How do I distinguish between voice chat rooms and video live rooms in the live room list?

`LiveListStore` does not differentiate between room business types. You must filter and categorize the list after fetching, at the application or UI layer.

We recommend two approaches:

**Approach 1 (Recommended): Use seatLayoutTemplateID for differentiation.**

This template ID defines the room layout. For supported template IDs and effects, refer to Run And Test.
- **Step 1: Specify ID when creating a room**

  - When calling `LiveListStore.shared.createLive`, set the `seatLayoutTemplateID` property of `LiveInfo` based on your business scenario:

  - Voice chat rooms: Use template IDs in the range 1–199.

  - Video live rooms: Use template IDs in the range 200–999.

- **Step 2: Filter when fetching the list**

  - On the client side, after receiving the list in `LiveListStore.state.liveList`, determine the business scenario by checking the template ID range.
      

      > **Note：**
      > 

      > If the seatLayoutTemplateID does not match your business scenario (voice chat room or video live room), seat layout features may not work as expected.
      > 

      **Approach 2:****Add a business prefix to **`liveID`**.**

      This is an optional, application-layer convention to help you filter rooms quickly.

- **Step 1: Add prefix when creating a room**

  - When generating liveID and calling createLive, assign different prefixes for each business type. For example: video live room IDs start with "Live_" (e.g., Live_12345), voice chat room IDs start with "voice_" (e.g., voice_67890).

- **Step 2: Check prefix when fetching the list**

  - On the client side, after fetching the list, distinguish rooms by checking the liveID prefix.

---

`LiveListStore` is the `AtomicXCore` core module for management of live room list, creation, joining and room status maintenance. With `LiveListStore`, you can build complete lifecycle management for your application.

## Core Features
- **Get live room list**: Obtain the current list of all public live rooms, supporting load by page.

- **Live stream lifecycle management**: Provides a complete process API for creation, going live, joining, leaving, and ending live stream.

- **Live stream information update**: Anchors can update publicly available information in the live streaming room at any time, such as cover and notice.

- **Real-time event monitoring**: Listen to key events such as live streaming end and users being kicked out.

- **Custom business data**: Powerful custom metadata (`MetaData`) capacity allows you to store and synchronize any business-relevant information in the room, such as live status, music info, and custom role.

## Core Concepts

Before starting integration, let's learn about several core concepts related to `LiveListStore` in the following table:
| **Core Concepts** | **Type** | **Core Responsibilities and Description** |
| --- | --- | --- |
| [LiveInfo](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveInfo-class.html) | `class` | Represents the information model of a live room. It contains live ID (`liveID`), name (`liveName`), room owner information (`liveOwner`) and custom metadata (`metaData`). |
| [LiveListState](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListState-class.html) | `class` | Represents the current status of the live list module. Its core attribute `liveList` is a `ValueListenable<List<LiveInfo>>` data type, storing the fetched live stream list. `currentLive` represents the live room information where the user currently resides. |
| [LiveListListener](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListListener-class.html) | `class` | Represents the global event listener for a live streaming room. It includes two callbacks, `onLiveEnded` (live streaming end) and `onKickedOutOfLive` (kicked out of live), used to process key room status updates. |
| [LiveListStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) | `class` | This is the core management class for interaction with the live list and room lifecycle. It is a Global Singleton (`shared`), responsible for all live streaming room operations such as create, join, and information update. |

## Implementation Steps

### Step 1: Integrating the Component
- **Live streaming**: Refer to quick integration with **AtomicXCore**, and complete the feature implementation for Anchor starts live streaming and audience viewing.

- **Voice chat room**: Refer to quick integration with **AtomicXCore**, and complete the feature implementation for Anchor starts live streaming and audience listening.

### Step 2: Audience Entering the Live Room Implementation

Create a page to display a live broadcast list. This page uses `GridView` to layout live streaming room cards. When a user clicks a certain card, get the `liveID` of the room and navigate to the audience viewing page.
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Live stream list page
class LiveListPage extends StatefulWidget {
  const LiveListPage({super.key});

  @override
  State<LiveListPage> createState() => _LiveListPageState();
}

class _LiveListPageState extends State<LiveListPage> {
  final _liveListStore = LiveListStore.shared;
  final ScrollController _scrollController = ScrollController();
  bool _isLoading = false;

  @override
  void initState() {
    super.initState();
    _liveListStore.liveState.liveList.addListener(_onLiveListChanged);
    _scrollController.addListener(_onScroll);
    _fetchLiveList();
  }

  void _onLiveListChanged() {
    setState(() {});
  }

  void _onScroll() {
    // Load more when scrolling to the bottom
    if (_scrollController.position.pixels >=
        _scrollController.position.maxScrollExtent - 200) {
      _loadMore();
    }
  }

  Future<void> _fetchLiveList() async {
    if (_isLoading) return;
    setState(() => _isLoading = true);

    final result = await _liveListStore.fetchLiveList(cursor: '', count: 20);
    if (!result.isSuccess) {
      debugPrint('List live stream failed: ${result.message}');
    }

    setState(() => _isLoading = false);
  }

  Future<void> _loadMore() async {
    if (_isLoading) return;

    final cursor = _liveListStore.liveState.liveListCursor.value;
    if (cursor.isEmpty) return; // no more data

    setState(() => _isLoading = true);
    await _liveListStore.fetchLiveList(cursor: cursor, count: 20);
    setState(() => _isLoading = false);
  }

  Future<void> _refresh() async {
    _liveListStore.reset();
    await _fetchLiveList();
  }

  // When user click certain card in the list
  void _onLiveCardTap(LiveInfo liveInfo) {
    // Create an audience viewing webpage and input the liveID
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => YourAudiencePage(liveID: liveInfo.liveID),
      ),
    );
  }

  @override
  void dispose() {
    _liveListStore.liveState.liveList.removeListener(_onLiveListChanged);
    _scrollController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    final liveList = _liveListStore.liveState.liveList.value;

    return Scaffold(
      appBar: AppBar(title: const Text('Live Stream List')),
      body: RefreshIndicator(
        onRefresh: _refresh,
        child: liveList.isEmpty
            ? Center(
                child: _isLoading
                    ? const CircularProgressIndicator()
                    const Text('No live stream')
              )
            : GridView.builder(
                controller: _scrollController,
                padding: const EdgeInsets.all(8),
                gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                  crossAxisCount: 2,
                  childAspectRatio: 0.75,
                  crossAxisSpacing: 8,
                  mainAxisSpacing: 8,
                ),
                itemCount: liveList.length + (_isLoading ? 1 : 0),
                itemBuilder: (context, index) {
                  if (index >= liveList.length) {
                    return const Center(child: CircularProgressIndicator());
                  }
                  return _buildLiveCard(liveList[index]);
                },
              ),
      ),
    );
  }

  Widget _buildLiveCard(LiveInfo liveInfo) {
    return GestureDetector(
      onTap: () => _onLiveCardTap(liveInfo),
      child: Card(
        clipBehavior: Clip.antiAlias,
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Cover image
            Expanded(
              child: Stack(
                fit: StackFit.expand,
                children: [
                  Image.network(
                    liveInfo.coverURL,
                    fit: BoxFit.cover,
                    errorBuilder: (context, error, stackTrace) {
                      return Container(color: Colors.grey[300]);
                    },
                  ),
                  // Live stream tag
                  Positioned(
                    top: 8,
                    left: 8,
                    child: Container(
                      padding: const EdgeInsets.symmetric(
                        horizontal: 6,
                        vertical: 2,
                      ),
                      decoration: BoxDecoration(
                        color: Colors.red,
                        borderRadius: BorderRadius.circular(4),
                      ),
                      child: const Text(
                        Live streaming
                        style: TextStyle(color: Colors.white, fontSize: 10),
                      ),
                    ),
                  ),
                  viewers
                  Positioned(
                    bottom: 8,
                    right: 8,
                    child: Container(
                      padding: const EdgeInsets.symmetric(
                        horizontal: 6,
                        vertical: 2,
                      ),
                      decoration: BoxDecoration(
                        color: Colors.black54,
                        borderRadius: BorderRadius.circular(4),
                      ),
                      child: Row(
                        mainAxisSize: MainAxisSize.min,
                        children: [
                          const Icon(
                            Icons.visibility,
                            color: Colors.white,
                            size: 12,
                          ),
                          const SizedBox(width: 4),
                          Text(
                            '${liveInfo.totalViewerCount}',
                            style: const TextStyle(
                              color: Colors.white,
                              fontSize: 10,
                            ),
                          ),
                        ],
                      ),
                    ),
                  ),
                ],
              ),
            ),
            // Live streaming information
            Padding(
              padding: const EdgeInsets.all(8),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    liveInfo.liveName,
                    maxLines: 1,
                    overflow: TextOverflow.ellipsis,
                    style: const TextStyle(fontWeight: FontWeight.bold),
                  ),
                  const SizedBox(height: 4),
                  Row(
                    children: [
                      CircleAvatar(
                        radius: 10,
                        backgroundImage: NetworkImage(
                          liveInfo.liveOwner.avatarURL,
                        ),
                      ),
                      const SizedBox(width: 4),
                      Expanded(
                        child: Text(
                          liveInfo.liveOwner.userName,
                          maxLines: 1,
                          overflow: TextOverflow.ellipsis,
                          style: TextStyle(
                            fontSize: 12,
                            color: Colors.grey[600],
                          ),
                        ),
                      ),
                    ],
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}

/// Audience viewing webpage (placeholder)
class YourAudiencePage extends StatelessWidget {
  final String liveID;

  const YourAudiencePage({super.key, required this.liveID});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Live Streaming Room')),
      body: Center(child: Text('Live Streaming Room: $liveID')),
    );
  }
}
```

**LiveInfo Parameter Description**
| **Parameter Name** | **Type** | **Description** |
| --- | --- | --- |
| `liveID` | `String` | Unique identifier of the live streaming room |
| `liveName` | `String` | Title of the live streaming room |
| `coverURL` | `String` | Thumbnail URL of the live streaming room |
| `liveOwner` | `LiveUserInfo` | Room owner's personal info |
| `totalViewerCount` | `int` | Total viewers in the live streaming room |
| `categoryList` | `List<int>` | Category tag list of the live streaming room |
| `notice` | `String` | Announcement information in the live streaming room |
| `metaData` | `Map<String, String>` | Custom metadata for complex business scenarios |

## Advanced Features

### Scenario One: Categorize Live Broadcast List

On the live square page of the App, the top section features category tags such as "Popular," "Music," and "Gaming." When users click different tags, the live stream list below dynamically filters to show only live streaming rooms of the corresponding category, thereby helping users quickly identify content of interest.

#### Implementation Method

The core is to use the `categoryList` property in the `LiveInfo` model. When the anchor starts live streaming and sets the category, the `LiveInfo` object returned by `fetchLiveList` will contain this classification information. After your App obtains the complete live list, just perform a simple filter on the client according to the user's selected category, then refresh the UI.

#### Sample Code

The following example shows how to create a `LiveListManager` to handle data and filter logic.
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Live stream list data manager
class LiveListManager extends ChangeNotifier {
  final _liveListStore = LiveListStore.shared;
  List<LiveInfo> _fullLiveList = [];
  List<LiveInfo> _filteredLiveList = [];
  int? _selectedCategoryId;

  List<LiveInfo> get filteredLiveList => _filteredLiveList;
  int? get selectedCategoryId => _selectedCategoryId;
  late final VoidCallback _liveListChangedListener = _onLiveListChanged;

  LiveListManager() {
    _liveListStore.liveState.liveList.addListener(_liveListChangedListener);
  }

  void _onLiveListChanged() {
    _fullLiveList = _liveListStore.liveState.liveList.value;
    _applyFilter();
  }

  Future<void> fetchFirstPage() async {
    _liveListStore.reset();
    await _liveListStore.fetchLiveList(cursor: '', count: 20);
  }

  /// Filter live stream list by category
  void filterLiveList({int? categoryId}) {
    _selectedCategoryId = categoryId;
    _applyFilter();
  }

  void _applyFilter() {
    if (_selectedCategoryId == null) {
      // If categoryId is null, display the complete list
      _filteredLiveList = List.from(_fullLiveList);
    } else {
      // Filter live streaming rooms by specified category
      _filteredLiveList = _fullLiveList.where((liveInfo) {
        return liveInfo.categoryList.contains(_selectedCategoryId);
      }).toList();
    }
    notifyListeners();
  }

  @override
  void dispose() {
    _liveListStore.liveState.liveList.removeListener(_liveListChangedListener);
    super.dispose();
  }
}
```
``` java
/// Live stream list webpage with category filtering
class CategoryLiveListPage extends StatefulWidget {
  const CategoryLiveListPage({super.key});

  @override
  State<CategoryLiveListPage> createState() => _CategoryLiveListPageState();
}

class _CategoryLiveListPageState extends State<CategoryLiveListPage> {
  final _manager = LiveListManager();
  late final VoidCallback _managerChangedListener = _onManagerChanged;

  // Classification list (example)
  final List<Map<String, dynamic>> _categories = [
    {'id': null, 'name': 'All'},
    {'id': 1, 'name': 'Music'},
    {'id': 2, 'name': 'Game'},
    {'id': 3, 'name': 'Chat'},
  ];

  @override
  void initState() {
    super.initState();
    _manager.addListener(_managerChangedListener);
    _manager.fetchFirstPage();
  }

  void _onManagerChanged() {
    setState(() {});
  }

  // When the user clicks the top category tag
  void _onCategoryTap(int? categoryId) {
    _manager.filterLiveList(categoryId: categoryId);
  }

  @override
  void dispose() {
    _manager.removeListener(_managerChangedListener);
    _manager.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Live Streaming Plaza')),
      body: Column(
        children: [
          // Category tag bar
          SizedBox(
            height: 50,
            child: ListView.builder(
              scrollDirection: Axis.horizontal,
              padding: const EdgeInsets.symmetric(horizontal: 8),
              itemCount: _categories.length,
              itemBuilder: (context, index) {
                final category = _categories[index];
                final isSelected = _manager.selectedCategoryId == category['id'];
                return Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 4),
                  child: ChoiceChip(
                    label: Text(category['name']),
                    selected: isSelected,
                    onSelected: (_) => _onCategoryTap(category['id']),
                  ),
                );
              },
            ),
          ),
          // Live stream list
          Expanded(
            child: _manager.filteredLiveList.isEmpty
                ? const Center(child: Text('No live stream'))
                : GridView.builder(
                    padding: const EdgeInsets.all(8),
                    gridDelegate:
                        const SliverGridDelegateWithFixedCrossAxisCount(
                      crossAxisCount: 2,
                      childAspectRatio: 0.75,
                      crossAxisSpacing: 8,
                      mainAxisSpacing: 8,
                    ),
                    itemCount: _manager.filteredLiveList.length,
                    itemBuilder: (context, index) {
                      final liveInfo = _manager.filteredLiveList[index];
                      return _buildLiveCard(liveInfo);
                    },
                  ),
          ),
        ],
      ),
    );
  }

  Widget _buildLiveCard(LiveInfo liveInfo) {
    return Card(
      clipBehavior: Clip.antiAlias,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Expanded(
            child: Image.network(
              liveInfo.coverURL,
              fit: BoxFit.cover,
              width: double.infinity,
              errorBuilder: (context, error, stackTrace) {
                return Container(color: Colors.grey[300]);
              },
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(8),
            child: Text(
              liveInfo.liveName,
              maxLines: 1,
              overflow: TextOverflow.ellipsis,
            ),
          ),
        ],
      ),
    );
  }
}
```

### Scenario Two: Show Product Information in Live Shopping

In an ecommerce live stream, the Anchor is explaining a product. At this point, a product card pops up at the bottom of the live stream for ALL audience, displaying the product image, name and price in real time. When the Anchor switches to the next product, the card on the client side updates automatically and synchronously.

#### Implementation Method

The Anchor sets the current product's structured information (recommend using **JSON** format) to a custom key (such as "`product_info`") through the `updateLiveMetaData` API setting. **AtomicXCore** will synchronize this update to ALL audience in real time. The client just needs to subscribe to `LiveListState.currentLive`, listen for changes in `metaData`, and once `product_info` is found updated, parse the JSON data and refresh the product card UI.

#### Sample Code
``` java
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Product Information Model
class Product {
  final String id;
  final String name;
  final String price;
  final String imageUrl;

  Product({
    required this.id,
    required this.name,
    required this.price,
    required this.imageUrl,
  });

  factory Product.fromJson(Map<String, dynamic> json) {
    return Product(
      id: json['id'] ?? '',
      name: json['name'] ?? '',
      price: json['price'] ?? '',
      imageUrl: json['imageUrl'] ?? '',
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'price': price,
      'imageUrl': imageUrl,
    };
  }
}

/// Anchor: Push product information
class HostProductController {
  final _liveListStore = LiveListStore.shared;

  Future<void> pushProductInfo(Product product) async {
    final jsonString = jsonEncode(product.toJson());
    final metaData = {'product_info': jsonString};

    // Use Global Singleton liveListStore to update metaData
    final result = await _liveListStore.updateLiveMetaData(metaData);
    if (result.isSuccess) {
      debugPrint('Product ${product.name} pushed successfully');
    } else {
      debugPrint('Product information sending failed: ${result.message}');
    }
  }
}

/// Client: Product card component
class ProductCardWidget extends StatefulWidget {
  const ProductCardWidget({super.key});

  @override
  State<ProductCardWidget> createState() => _ProductCardWidgetState();
}

class _ProductCardWidgetState extends State<ProductCardWidget> {
  final _liveListStore = LiveListStore.shared;
  Product? _currentProduct;
  String? _lastProductInfo;
  late final VoidCallback _currentLiveChangedListener = _onCurrentLiveChanged;

  @override
  void initState() {
    super.initState();
    _liveListStore.liveState.currentLive.addListener(_currentLiveChangedListener);
  }

  void _onCurrentLiveChanged() {
    final currentLive = _liveListStore.liveState.currentLive.value;
    final productInfo = currentLive.metaData['product_info'];

    // Check whether changed
    if (productInfo != _lastProductInfo) {
      _lastProductInfo = productInfo;
      _parseProductInfo(productInfo);
    }
  }

  void _parseProductInfo(String? jsonString) {
    if (jsonString == null || jsonString.isEmpty) {
      setState(() => _currentProduct = null);
      return;
    }

    try {
      final json = jsonDecode(jsonString) as Map<String, dynamic>;
      final product = Product.fromJson(json);
      setState(() => _currentProduct = product);
    } catch (e) {
      debugPrint('Failed to parse product information: $e');
    }
  }

  @override
  void dispose() {
    _liveListStore.liveState.currentLive.removeListener(_currentLiveChangedListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    if (_currentProduct == null) {
      return const SizedBox.shrink();
    }

    return Container(
      margin: const EdgeInsets.all(16),
      padding: const EdgeInsets.all(12),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(12),
        boxShadow: [
          BoxShadow(
            color: Colors.black.withOpacity(0.1),
            blurRadius: 8,
            offset: const Offset(0, 2),
          ),
        ],
      ),
      child: Row(
        children: [
          product image
          ClipRRect(
            borderRadius: BorderRadius.circular(8),
            child: Image.network(
              _currentProduct!.imageUrl,
              width: 80,
              height: 80,
              fit: BoxFit.cover,
              errorBuilder: (context, error, stackTrace) {
                return Container(
                  width: 80,
                  height: 80,
                  color: Colors.grey[300],
                  child: const Icon(Icons.image),
                );
              },
            ),
          ),
          const SizedBox(width: 12),
          product information
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              mainAxisSize: MainAxisSize.min,
              children: [
                Text(
                  _currentProduct!.name,
                  style: const TextStyle(
                    fontSize: 14,
                    fontWeight: FontWeight.bold,
                  ),
                  maxLines: 2,
                  overflow: TextOverflow.ellipsis,
                ),
                const SizedBox(height: 4),
                Text(
                  '¥${_currentProduct!.price}',
                  style: const TextStyle(
                    fontSize: 16,
                    color: Colors.red,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ],
            ),
          ),
          purchase button
          ElevatedButton(
            onPressed: () {
              // Implement purchase logic
              debugPrint('Purchase goods: ${_currentProduct!.name}');
            },
            style: ElevatedButton.styleFrom(
              backgroundColor: Colors.orange,
              foregroundColor: Colors.white,
            ),
            child: const Text('Buy now'),
          ),
        ],
      ),
    );
  }
}
```

## API documentation

For detailed information about ALL public interfaces, properties and methods of [LiveListStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) and its related classes, please refer to the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework. The related Store used in this document is as follows:
| **Store/Component** | **Feature Description** | **API Reference** |
| --- | --- | --- |
| **LiveCoreWidget** | The core view component for live video stream display and interaction: responsible for video stream rendering and view widget processing, supporting live streaming, audience mic connection, Anchor Connection (TUILiveKit), and other scenarios. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html) |
| **LiveCoreController** | Controller for LiveCoreWidget: used to set up live streaming ID, control preview, and perform other operations. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html) |
| **LiveListStore** | Full lifecycle management of live streaming room: create/join/leave/terminate room, query room list, modify live information (name, notice), listen to live streaming status (for example being kicked out, ended). | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) |

## FAQs

### What Are the Limitations and Rules to Note When Using `UpdateLiveMetaData`?

To ensure system stability and efficiency, the usage of `metaData` follows the following rules:
- **Permission**: Only the room owner and admin can call the API `updateLiveMetaData`. General audience has no permission.

- **Quantity and size limit: **

  - A single room supports up to **10** keys.

  - The length of each key does not exceed **50 bytes**, and the length of each value does not exceed **2KB**.

  - The total size of ALL values in a single room is no more than **16KB**.

- **Conflict resolution**: The update mechanism for `metaData` is "last write wins". If multiple administrators modify the same key in a short time frame, the last modification will take effect. It is advisable to avoid multiple users simultaneously adjusting the same key information in service design.

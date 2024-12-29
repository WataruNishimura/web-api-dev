<script lang="ts">
	const connection = window.navigator.connection;

	if (!connection) {
		console.log('Connection API is not supported');
	} else {
		function updateConnectionStatus(connection: NetworkInformation) {
			let type = connection.effectiveType;
			console.log(`接続の種類が ${type} から ${connection.effectiveType} に変化`);
			type = connection.effectiveType;
		}

		connection.addEventListener('change', () => {
			updateConnectionStatus(connection);
		});
	}
</script>

<div>
	{#if connection}
		<p>接続の種類: {connection.effectiveType}</p>
		<p>ダウンロード速度: {connection.downlink} Mbps</p>
		<p>最大ダウンロード速度: {connection.downlinkMax}</p>
		<p>ラウンドトリップ時間: {connection.rtt} ms</p>
		<p>ユーザーセーブデータステータス: {connection.saveData ? '有効' : '無効'}</p>
		<div>
			{#if connection.effectiveType === '2g' || connection.effectiveType === 'slow-2g' || connection.effectiveType === '3g'}
				<p>接続が遅いため、画像を表示しません</p>
			{:else}
				<img
					src="https://picsum.photos/4096/2304"
					width="640"
					height="360"
					alt="ランダムなサイズの大きい画像"
				/>
			{/if}
		</div>
	{:else}
		<p>Connection API はサポートされていません</p>
		<p>Google ChromeもしくはChromium系ブラウザを利用してください</p>
	{/if}
</div>
